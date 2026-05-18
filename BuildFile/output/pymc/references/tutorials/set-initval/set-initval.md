# How To: Set Initval

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test set initval

## Prerequisites

**Required Modules:**
- `copy`
- `pickle`
- `threading`
- `traceback`
- `warnings`
- `unittest.mock`
- `arviz`
- `cloudpickle`
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pytensor`
- `pytensor.sparse`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.sparse`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.link.numba`
- `pytensor.raise_op`
- `pytensor.tensor.random.op`
- `pytensor.tensor.variable`
- `pymc`
- `pymc`
- `pymc.blocking`
- `pymc.distributions`
- `pymc.distributions.distribution`
- `pymc.distributions.transforms`
- `pymc.exceptions`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.variational.minibatch_rv`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(392)
```

**Verification:**
```python
assert np.array_equal(model.rvs_to_initial_values[mu], np.array([[100.0]]))
```

### Step 2: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(model.rvs_to_initial_values[alpha], np.array(100))
```

**Verification:**
```python
assert model.rvs_to_initial_values[value] is None
```

### Step 3: Assign eta = pm.Uniform(...)

```python
eta = pm.Uniform('eta', 1.0, 2.0, size=(1, 1))
```

**Verification:**
```python
assert y in model.rvs_to_initial_values
```

### Step 4: Assign mu = pm.Normal(...)

```python
mu = pm.Normal('mu', sigma=eta, initval=[[100]])
```

### Step 5: Assign alpha = pm.HalfNormal(...)

```python
alpha = pm.HalfNormal('alpha', initval=100)
```

### Step 6: Assign value = pm.NegativeBinomial(...)

```python
value = pm.NegativeBinomial('value', mu=mu, alpha=alpha)
```

### Step 7: Assign x = pm.Flat(...)

```python
x = pm.Flat('x')
```

### Step 8: Assign y = pm.Normal(...)

```python
y = pm.Normal('y', x, 1)
```


## Complete Example

```python
# Workflow
rng = np.random.RandomState(392)
with pm.Model() as model:
    eta = pm.Uniform('eta', 1.0, 2.0, size=(1, 1))
    mu = pm.Normal('mu', sigma=eta, initval=[[100]])
    alpha = pm.HalfNormal('alpha', initval=100)
    value = pm.NegativeBinomial('value', mu=mu, alpha=alpha)
assert np.array_equal(model.rvs_to_initial_values[mu], np.array([[100.0]]))
np.testing.assert_array_equal(model.rvs_to_initial_values[alpha], np.array(100))
assert model.rvs_to_initial_values[value] is None
with pm.Model() as model:
    x = pm.Flat('x')
    y = pm.Normal('y', x, 1)
assert y in model.rvs_to_initial_values
```

## Next Steps


---

*Source: test_core.py:808 | Complexity: Advanced | Last updated: 2026-05-18*