# How To: Linear Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test linear model

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `arviz_base`
- `arviz_base.testing`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pytensor.graph.traversal`
- `pytensor.tensor.variable`
- `scipy`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.shape_utils`
- `pymc.exceptions`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign unknown = compile_forward_sampling_function(...)

```python
f, volatile_rvs = compile_forward_sampling_function([obs], vars_in_trace=[alpha, beta, sigma, mu], basic_rvs=model.basic_RVs)
```

**Verification:**
```python
assert volatile_rvs == {obs}
```

### Step 2: Assign x = pm.Data(...)

```python
x = pm.Data('x', np.linspace(0, 1, 10))
```

**Verification:**
```python
assert {i.name for i in self.get_function_inputs(f)} == {'alpha', 'beta', 'sigma'}
```

### Step 3: Assign y = pm.Data(...)

```python
y = pm.Data('y', np.ones(10))
```

**Verification:**
```python
assert {i.name for i in self.get_function_roots(f)} == {'x', 'alpha', 'beta', 'sigma'}
```

### Step 4: Assign alpha = pm.Normal(...)

```python
alpha = pm.Normal('alpha', 0, 0.1)
```

### Step 5: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 0.1)
```

### Step 6: Assign mu = pm.Deterministic(...)

```python
mu = pm.Deterministic('mu', alpha + beta * x)
```

### Step 7: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', 0.1)
```

### Step 8: Assign obs = pm.Normal(...)

```python
obs = pm.Normal('obs', mu, sigma, observed=y, shape=x.shape)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    x = pm.Data('x', np.linspace(0, 1, 10))
    y = pm.Data('y', np.ones(10))
    alpha = pm.Normal('alpha', 0, 0.1)
    beta = pm.Normal('beta', 0, 0.1)
    mu = pm.Deterministic('mu', alpha + beta * x)
    sigma = pm.HalfNormal('sigma', 0.1)
    obs = pm.Normal('obs', mu, sigma, observed=y, shape=x.shape)
f, volatile_rvs = compile_forward_sampling_function([obs], vars_in_trace=[alpha, beta, sigma, mu], basic_rvs=model.basic_RVs)
assert volatile_rvs == {obs}
assert {i.name for i in self.get_function_inputs(f)} == {'alpha', 'beta', 'sigma'}
assert {i.name for i in self.get_function_roots(f)} == {'x', 'alpha', 'beta', 'sigma'}
```

## Next Steps


---

*Source: test_forward.py:135 | Complexity: Advanced | Last updated: 2026-05-18*