# pymc Documentation Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. Implementing a RandomVariable Distribution #3

- Kind: `documentation`
- Source: `references/documentation/other/implementing_distribution.md`
- Note: Documentation code block extracted for implementation use.

```python
import pytensor.tensor as pt
from pymc.distributions.continuous import PositiveContinuous
from pymc.distributions.dist_math import check_parameters
from pymc.distributions.shape_utils import rv_size_is_none


# Subclassing `PositiveContinuous` will dispatch a default `log` transformation
class Blah(PositiveContinuous):
    # This will be used by the metaclass `DistributionMeta` to dispatch the
    # class `logp` and `logcdf` methods to the `blah` `Op` defined in the last line of the code above.
    rv_op = blah

    # dist() is responsible for returning an instance of the rv_op.
    # We pass the standard parametrizations to super().dist
    @classmethod
    def dist(cls, param1, param2=None, alt_param2=None, **kwargs):
        param1 = pt.as_tensor_variable(param1)
        if param2 is not None and alt_param2 is not None:
            raise ValueError("Only one of param2 and alt_param2 is allowed.")
        if alt_param2 is not None:
            param2 = 1 / alt_param2
        param2 = pt.as_tensor_variable(param2)

        # The first value-only argument should be a list of the parameters that
        # the rv_op needs in order to be instantiated
        return super().dist([param1, param2], **kwargs)

    # support_point returns a symbolic expression for the stable point from which to start sampling
    # the variable, given the implicit `rv`, `size` and `param1` ... `paramN`.
    # This is typically a "representative" point such as the the mean or mode.
    def support_point(rv, size, param1, param2):
        support_point, _ = pt.broadcast_arrays(param1, param2)
        if not rv_size_is_none(size):
            support_point = pt.full(size, support_point)
        return support_point

    # Logp returns a symbolic expression for the elementwise log-pdf or log-pmf evaluation
    # of the variable given the `value` of the variable and the parameters `param1` ... `paramN`.
    def logp(value, param1, param2):
        logp_expression = value * (param1 + pt.log(param2))

        # A switch is often used to enforce the distribution support domain
        bounded_logp_expression = pt.switch(
            pt.gt(value >= 0),
            logp_expression,
            -np.inf,
        )

        # We use `check_parameters` for parameter validation. After the default expression,
        # multiple comma-separated symbolic conditions can be added.
        # Whenever a bound is invalidated, the returned expression raises an error
        # with the message defined in the optional `msg` keyword argument.
        return check_parameters(
            bounded_logp_expression,
            param2 >= 0,
            msg="param2 >= 0",
        )

    # logcdf works the same way as logp. For bounded variables, it is expected to return
    # `-inf` for values below the domain start and `0` for values above the domain end.
    def logcdf(value, param1, param2):
        ...

    def icdf(value, param1, param2):
        ...
```

## 2. Implementing a RandomVariable Distribution #1

- Kind: `documentation`
- Source: `references/documentation/other/implementing_distribution.md`
- Note: Documentation code block extracted for implementation use.

```python
from pytensor.tensor.var import TensorVariable
from pytensor.tensor.random.op import RandomVariable
from typing import List, Tuple

# Create your own `RandomVariable`...
class BlahRV(RandomVariable):
    name: str = "blah"

    # Provide a numpy-style signature for this RV, which indicates
    # the number and core dimensionality of each input and output.
    signature: "(),()->()"

    # The NumPy/PyTensor dtype for this RV (e.g. `"int32"`, `"int64"`).
    # The standard in the library is `"int64"` for discrete variables
    # and `"floatX"` for continuous variables
    dtype: str = "floatX"

    # A pretty text and LaTeX representation for the RV
    _print_name: Tuple[str, str] = ("blah", "\\operatorname{blah}")

    # If you want to add a custom signature and default values for the
    # parameters, do it like this. Otherwise this can be left out.
    def __call__(self, loc=0.0, scale=1.0, **kwargs) -> TensorVariable:
        return super().__call__(loc, scale, **kwargs)

    # This is the Python code that produces samples.  Its signature will always
    # start with a NumPy `RandomState` object, then the distribution
    # parameters, and, finally, the size.

    @classmethod
    def rng_fn(
        cls,
        rng: np.random.RandomState,
        loc: np.ndarray,
        scale: np.ndarray,
        size: Tuple[int, ...],
    ) -> np.ndarray:
        return scipy.stats.blah.rvs(loc, scale, random_state=rng, size=size)

# Create the actual `RandomVariable` `Op`...
blah = BlahRV()
```

## 3. Glossary #1

- Kind: `documentation`
- Source: `references/documentation/other/glossary.md`
- Note: Documentation code block extracted for implementation use.

```text
unnamed_distribution
    PyMC distributions can be initialized directly (e.g. `pm.Normal`) or using the `.dist` classmethod (e.g. `pm.Normal.dist`). Distributions initialized with the 1st method are registered as model parameters and thus, need to be given a name and be initialized within a model context. "unnamed_distributions" are distributions initialized with the 2nd method. These are standalone distributions, they are not parameters in any model and can be used to draw samples from a distribution by itself or as parameters to other distributions like mixtures or censored.

    "unnamed_distributions" can be used outside the model context. For example:
```

## 4. Readme

- Kind: `documentation`
- Source: `references/documentation/overview/README.rst`
- Note: Documentation code block extracted for implementation use.

```bash
x = Normal('x',0,1)
x_dist = pm.Normal.dist(shape=(100, 3))
x_data = pm.draw(x_dist, random_seed=seed)
x = pm.Data("x", x_data, dims=["trial", "features"])
betas = pm.Normal("betas", dims="features")
sigma = pm.HalfNormal("sigma")
plant_growth = pm.Normal("plant growth", mu, sigma, dims="trial")
idata = pm.sample_prior_predictive(random_seed=seed) # Sample from prior predictive distribution.
idata = pm.sample(random_seed=seed)
summary = pm.stats.summary(idata, var_names=["betas", "sigma"])
new_x_data = pm.draw(
new_predictions = pm.sample_posterior_predictive(
```

## 5. Implementing a RandomVariable Distribution #2

- Kind: `documentation`
- Source: `references/documentation/other/implementing_distribution.md`
- Note: Documentation code block extracted for implementation use.

```python
# blah = pytensor.tensor.random.uniform in this example
# multiple calls with the same seed should return the same values
pm.draw(blah([0, 0], [1, 2], size=(10, 2)), random_seed=1)

# array([[0.83674527, 0.76593773],
#    [0.00958496, 1.85742402],
#    [0.74001876, 0.6515534 ],
#    [0.95134629, 1.23564938],
#    [0.41460156, 0.33241175],
#    [0.66707807, 1.62134924],
#    [0.20748312, 0.45307477],
#    [0.65506507, 0.47713784],
#    [0.61284429, 0.49720329],
#    [0.69325978, 0.96272673]])
```

## 6. Jupyter Style Guide #3

- Kind: `documentation`
- Source: `references/documentation/other/jupyter_style.md`
- Note: Documentation code block extracted for implementation use.

```text
:::
  ::::

  This makes editing the code if restructuring the subplots easier, only one change per subplot
  is needed instead of one change per matplotlib function call.

* It is often useful to make a numpy linspace into an {class}`~xarray.DataArray`
  for xarray to handle aligning and broadcasting automatically and ease computation.
  * If a dimension name is needed, use `x_plot`
  * If a variable name is needed for the original array and DataArray to coexist, add `_da` suffix

  Thus, ending up with code like:
```

## 7. PyMC Developer Guide #2

- Kind: `documentation`
- Source: `references/documentation/other/developer_guide.md`
- Note: Documentation code block extracted for implementation use.

```python
with pm.Model():
    z = pm.Normal("z", 0, 5)
print(type(z.owner.op))
# ==> pytensor.tensor.random.basic.NormalRV
isinstance(z.owner.op, pytensor.tensor.random.basic.RandomVariable)
# ==> True
```

## 8. Architecture #1

- Kind: `documentation`
- Source: `references/documentation/architecture/ARCHITECTURE.md`
- Note: Documentation code block extracted for implementation use.

```python
with pm.Model() as model:
  theta = pm.Beta("theta", alpha=1, beta=2)
  p = pm.Beta("n", p=theta, n=2, observed=[1,2])
  inf_data = pm.sample()
```

## 9. PyMC Developer Guide #3

- Kind: `documentation`
- Source: `references/documentation/other/developer_guide.md`
- Note: Documentation code block extracted for implementation use.

```python
with pm.Model():
    z = pm.Normal("z", 0, 5)
symbolic = pm.logp(z, 2.5)
numeric = symbolic.eval()
# array(-2.65337645)
```

## 10. Jupyter Style Guide #2

- Kind: `documentation`
- Source: `references/documentation/other/jupyter_style.md`
- Note: Documentation code block extracted for implementation use.

```text
x = np.array(...)
  with pm.Model():
      x_ = pm.Data("x", x)
      ...
```
