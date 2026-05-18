---
name: pymc
description: Local codebase analysis for pymc
doc_version: 
---

# pymc Codebase

## Description

Local codebase analysis and documentation generated from code analysis.

**Path:** `pymc`
**Files Analyzed:** 0
**Languages:** 
**Analysis Depth:** surface

## When to Use This Skill

Use this skill when you need to:
- Understand the codebase architecture and design patterns
- Find implementation examples and usage patterns
- Review API documentation extracted from code
- Check configuration patterns and best practices
- Explore test examples and real-world usage
- Navigate the codebase structure efficiently

## ⚡ Quick Reference

### Codebase Statistics

**Languages:**

**Analysis Performed:**
- ✅ API Reference (C2.5)
- ✅ Dependency Graph (C2.6)
- ✅ Design Patterns (C3.1)
- ✅ Test Examples (C3.2)
- ✅ Configuration Patterns (C3.4)
- ✅ Architectural Analysis (C3.7)
- ✅ Project Documentation (C3.9)

### 🎨 Design Patterns Detected

*From C3.1 codebase analysis (confidence > 0.7)*

- **Adapter**: 8 instances

*Total: 8 high-confidence patterns*

*See `references/patterns/` for complete pattern analysis*

## 📝 Code Examples

*High-quality examples extracted from test files (C3.2)*

**Workflow: test build constant data** (complexity: 1.00)

```python
with pm.Model() as model:
    model.add_coord('length_coord', length=1)
    model.add_coord('value_coord', values=(3,))
    x = pm.Data('x', np.array([1.0, 2.0, 3.0]))
length_var = model.dim_lengths['length_coord']
value_var = model.dim_lengths['value_coord']
trace_constant_data = {'x': np.array([1.0, 2.0, 3.0])}
trace_coords_same = {'length_coord': np.array([0]), 'value_coord': np.array([3])}
constant_data_same = _build_constant_data(trace_constant_data, trace_coords_same, model)
assert set(constant_data_same) == {x, length_var, value_var}
trace_coords_diff = {'length_coord': np.array([0, 1]), 'value_coord': np.array([4])}
constant_data_diff = _build_constant_data(trace_constant_data, trace_coords_diff, model)
assert set(constant_data_diff) == {x}
constant_data_no_x = _build_constant_data({}, trace_coords_same, model)
assert x not in constant_data_no_x
assert set(constant_data_no_x) == {length_var, value_var}
```

**Workflow: test get vars in point list** (complexity: 1.00)

```python
with pm.Model() as modelA:
    pm.Normal('a', 0, 1)
    pm.Normal('b', 0, 1)
    pm.Normal('d', 0, 1)
with pm.Model() as modelB:
    a = pm.Normal('a', 0, 1)
    pm.Normal('c', 0, 1)
    pm.Data('d', 0)
point_list = [{'a': 0, 'b': 0, 'd': 0}]
vars_in_trace = get_vars_in_point_list(point_list, modelB)
assert set(vars_in_trace) == {a}
strace = pm.backends.NDArray(model=modelB, vars=modelA.free_RVs)
strace.setup(1, 1)
strace.values = point_list[0]
strace.draw_idx = 1
trace = MultiTrace([strace])
vars_in_trace = get_vars_in_point_list(trace, modelB)
assert set(vars_in_trace) == {a}
```

**Workflow: test vectorize over posterior with intermediate rvs** (complexity: 1.00)

```python
with pm.Model() as model:
    a = pm.Normal('a')
    b = pm.Normal.dist(a)
    c = b + 1
    d = pm.Normal.dist(c)
    idata = pm.sample_prior_predictive(100, var_names=['a'])
    idata.update({'posterior': idata.prior})
_, _, vectorized_no_intermediate = vectorize_over_posterior(outputs=[b, c, d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
[vectorized_intermediate_rvs] = vectorize_over_posterior(outputs=[d], posterior=idata.posterior, input_rvs=[a], allow_rvs_in_graph=True)
assert vectorized_no_intermediate.type.shape == (1, 100)
assert vectorized_no_intermediate.type.shape == vectorized_intermediate_rvs.type.shape
[a_ancestor1] = get_var_by_name([vectorized_no_intermediate], 'a')
[a_ancestor2] = get_var_by_name([vectorized_intermediate_rvs], 'a')
assert isinstance(a_ancestor1, TensorConstant)
assert np.array_equiv(a_ancestor1.eval(), idata.posterior.a.data)
assert isinstance(a_ancestor2, TensorConstant)
assert np.array_equiv(a_ancestor2.eval(), idata.posterior.a.data)
```

**Workflow: Test whether the logprob for ```pt.max``` produces the corrected

The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:
    U_1, \dots, U_n \stackrel{      ext{i.i.d.}}{\sim}      ext{Uniform}(0, 1) \Rightarrow U_{(k)} \sim     ext{Beta}(k, n + 1- k)
for all 1<=k<=n** (complexity: 1.00)

```python
'Test whether the logprob for ```pt.max``` produces the corrected\n\n    The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:\n        U_1, \\dots, U_n \\stackrel{\text{i.i.d.}}{\\sim} \text{Uniform}(0, 1) \\Rightarrow U_{(k)} \\sim \text{Beta}(k, n + 1- k)\n    for all 1<=k<=n\n    '
x = pt.random.uniform(0, 1, size=shape)
x.name = 'x'
x_max = pt.max(x, axis=axis)
x_max_value = pt.scalar('x_max_value')
x_max_logprob = logp(x_max, x_max_value)
assert_no_rvs(x_max_logprob)
test_value = value
n = np.prod(shape)
beta_rv = pt.random.beta(n, 1, name='beta')
beta_vv = beta_rv.clone()
beta_rv_logprob = logp(beta_rv, beta_vv)
np.testing.assert_allclose(beta_rv_logprob.eval({beta_vv: test_value}), x_max_logprob.eval({x_max_value: test_value}), rtol=1e-06)
```

**Workflow: Test whether the logprob for ```pt.mix``` produces the corrected
The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:
    U_1, \dots, U_n \stackrel{      ext{i.i.d.}}{\sim}      ext{Uniform}(0, 1) \Rightarrow U_{(k)} \sim     ext{Beta}(k, n + 1- k)
for all 1<=k<=n** (complexity: 1.00)

```python
'Test whether the logprob for ```pt.mix``` produces the corrected\n    The fact that order statistics of i.i.d. uniform RVs ~ Beta is used here:\n        U_1, \\dots, U_n \\stackrel{\text{i.i.d.}}{\\sim} \text{Uniform}(0, 1) \\Rightarrow U_{(k)} \\sim \text{Beta}(k, n + 1- k)\n    for all 1<=k<=n\n    '
x = pt.random.uniform(0, 1, size=shape)
x.name = 'x'
x_min = pt.min(x, axis=axis)
x_min_value = pt.scalar('x_min_value')
x_min_logprob = logp(x_min, x_min_value)
assert_no_rvs(x_min_logprob)
test_value = value
n = np.prod(shape)
beta_rv = pt.random.beta(1, n, name='beta')
beta_vv = beta_rv.clone()
beta_rv_logprob = logp(beta_rv, beta_vv)
np.testing.assert_allclose(beta_rv_logprob.eval({beta_vv: test_value}), x_min_logprob.eval({x_min_value: test_value}), rtol=1e-06)
```

**Workflow: test switch non overlapping logp matches change of variables** (complexity: 1.00)

```python
scale = pt.scalar('scale')
x = pm.Normal.dist(mu=0, sigma=1, size=(3,))
y = pt.switch(x > 0, x, scale * x)
vv = pt.vector('vv')
logp_y = logp(y, vv)
inv = pt.switch(pt.gt(vv, 0), vv, vv / scale)
expected = logp(x, inv) + pt.switch(pt.gt(vv, 0), 0.0, -pt.log(scale))
logp_y_fn = function([vv, scale], logp_y)
expected_fn = function([vv, scale], expected)
v = np.array([-2.0, 0.0, 1.5])
np.testing.assert_allclose(logp_y_fn(v, 0.5), expected_fn(v, 0.5))
with pytest.raises(ParameterValueError, match='switch non-overlapping scale > 0'):
    logp_y_fn(v, -0.5)
with pytest.raises(ParameterValueError, match='switch non-overlapping scale > 0'):
    logp_y_fn(v, 0.0)
```

**Workflow: test all distributions have support points** (complexity: 1.00)

```python
import pymc.distributions as dist_module
from pymc.distributions.distribution import DistributionMeta
dists = (getattr(dist_module, dist) for dist in dist_module.__all__)
dists = (dist for dist in dists if isinstance(dist, DistributionMeta))
generic_func = _support_point.dispatch(object)
missing_support_points = {dist for dist in dists if getattr(dist, 'rv_type', None) is not None and _support_point.dispatch(dist.rv_type) is generic_func}
missing_support_points -= {dist_module.Distribution, dist_module.Discrete, dist_module.Continuous, dist_module.CustomDist, dist_module.simulator.Simulator}
not_implemented = {dist_module.timeseries.EulerMaruyama}
unexpected_implemented = not_implemented - missing_support_points
if unexpected_implemented:
    raise Exception(f'Distributions {unexpected_implemented} have a `support_point` implemented. This test must be updated to expect this.')
unexpected_not_implemented = missing_support_points - not_implemented
if unexpected_not_implemented:
    raise NotImplementedError(f'Unexpected by this test, distributions {unexpected_not_implemented} do not have a `support_point` implementation. Either add a support_point or filter these distributions in this test.')
```

**Workflow: Test that we can recreate a SymbolicRandomVariable with new RNG inputs.

Related to https://github.com/pymc-devs/pytensor/issues/473** (complexity: 1.00)

```python
'Test that we can recreate a SymbolicRandomVariable with new RNG inputs.\n\n        Related to https://github.com/pymc-devs/pytensor/issues/473\n        '
rng = pytensor.shared(np.random.default_rng())
dummy_rng = rng.type()
dummy_next_rng, dummy_x = pt.random.normal(rng=dummy_rng).owner.outputs
op = SymbolicRandomVariable([dummy_rng], [dummy_next_rng, dummy_x], ndim_supp=0)
next_rng, x = op(rng)
assert op.update(x.owner) == {rng: next_rng}
new_rng = pytensor.shared(np.random.default_rng())
inputs = x.owner.inputs.copy()
inputs[0] = new_rng
new_next_rng, new_x = x.owner.op(*inputs)
assert op.update(new_x.owner) == {new_rng: new_next_rng}
```

**Workflow: test univariate** (complexity: 1.00)

```python
data = np.array([0.25, 0.5, 0.25])
mask = np.array([False, False, True])
rv = pm.Normal.dist([1, 2, 3])
if symbolic_rv:
    rv = pm.Censored.dist(rv, lower=-100, upper=100)
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
if symbolic_rv:
    assert isinstance(obs_rv.owner.op, PartialObservedRV)
    assert isinstance(unobs_rv.owner.op, PartialObservedRV)
else:
    assert isinstance(obs_rv.owner.op, Normal)
    assert isinstance(unobs_rv.owner.op, Normal)
assert tuple(obs_rv.shape.eval()) == (2,)
assert tuple(unobs_rv.shape.eval()) == (1,)
assert tuple(joined_rv.shape.eval()) == (3,)
logp = conditional_logp({obs_rv: pt.as_tensor(data[~mask]), unobs_rv: pt.as_tensor(data[mask])})
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
np.testing.assert_allclose(obs_logp, st.norm([1, 2]).logpdf([0.25, 0.5]))
np.testing.assert_allclose(unobs_logp, st.norm([3]).logpdf([0.25]))
```

**Workflow: test multivariate constant mask unseparable** (complexity: 1.00)

```python
mask = pt.constant(np.array([[True, True, False, False]]))
obs_data = np.array([[0.1, 0.4, 0.1, 0.4]])
unobs_data = np.array([[0.4, 0.1, 0.4, 0.1]])
rv = pm.Dirichlet.dist([1, 2, 3, 4], shape=(1, 4))
(obs_rv, obs_mask), (unobs_rv, unobs_mask), joined_rv = create_partial_observed_rv(rv, mask)
assert isinstance(obs_rv.owner.op, PartialObservedRV)
assert isinstance(unobs_rv.owner.op, PartialObservedRV)
assert tuple(obs_rv.shape.eval()) == (2,)
assert tuple(unobs_rv.shape.eval()) == (2,)
assert tuple(joined_rv.shape.eval()) == (1, 4)
logp = conditional_logp({obs_rv: pt.as_tensor(obs_data)[obs_mask], unobs_rv: pt.as_tensor(unobs_data)[unobs_mask]})
obs_logp, unobs_logp = pytensor.function([], list(logp.values()))()
expected_logp = pm.logp(rv, [[0.1, 0.4, 0.4, 0.1]]).eval()
np.testing.assert_almost_equal(obs_logp, expected_logp)
np.testing.assert_array_equal(unobs_logp, [])
```

*See `references/test_examples/` for all extracted examples*

## ⚙️ Configuration Patterns

*From C3.4 configuration analysis*

**Configuration Files Analyzed:** 31
**Total Settings:** 262
**Patterns Detected:** 0

**Configuration Types:**
- unknown: 31 files

*See `references/config_patterns/` for detailed configuration analysis*

## 📖 Project Documentation

*Extracted from markdown files in the project (C3.9)*

**Total Documentation Files:** 77
**Categories:** 8

### Overview

- **GOVERNANCE.md** (`GOVERNANCE.md`)
- **README.rst** (`README.rst`)

### Architecture

- **ARCHITECTURE.md** (`ARCHITECTURE.md`)

### Guides

- **Gaussian_Processes.rst** (`docs/source/guides/Gaussian_Processes.rst`)
- **Probability_Distributions.rst** (`docs/source/guides/Probability_Distributions.rst`)

### Api

- **backends.rst** (`docs/source/api/backends.rst`)
- **data.rst** (`docs/source/api/data.rst`)
- **distributions.rst** (`docs/source/api/dims/distributions.rst`)
- **math.rst** (`docs/source/api/dims/math.rst`)
- **model.rst** (`docs/source/api/dims/model.rst`)
- *...and 36 more*

### Community

- **CODE_OF_CONDUCT.md** (`CODE_OF_CONDUCT.md`)

### Contributing

- **CONTRIBUTING.md** (`CONTRIBUTING.md`)

*See `references/documentation/` for all project documentation*

## 📚 Available References

This skill includes detailed reference documentation:

- **Dependencies**: `references/dependencies/` - Dependency graph and analysis
- **Patterns**: `references/patterns/` - Detected design patterns
- **Examples**: `references/test_examples/` - Usage examples from tests
- **Configuration**: `references/config_patterns/` - Configuration patterns
- **Documentation**: `references/documentation/` - Project documentation

---

**Generated by Skill Seeker** | Codebase Analyzer with C3.x Analysis
