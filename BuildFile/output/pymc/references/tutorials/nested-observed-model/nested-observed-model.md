# How To: Nested Observed Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nested observed model

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
f, volatile_rvs = compile_forward_sampling_function(outputs=model.observed_RVs, vars_in_trace=[beta, mu, sigma], basic_rvs=model.basic_RVs)
```

**Verification:**
```python
assert volatile_rvs == {category, beta, obs}
```

### Step 2: Assign unknown = compile_forward_sampling_function(...)

```python
f, volatile_rvs = compile_forward_sampling_function(outputs=model.observed_RVs, vars_in_trace=[beta, mu, sigma], constant_data={p: p.get_value()}, basic_rvs=model.basic_RVs)
```

**Verification:**
```python
assert {i.name for i in self.get_function_inputs(f)} == {'sigma'}
```

### Step 3: Assign p = pm.Data(...)

```python
p = pm.Data('p', np.array([0.25, 0.5, 0.25]))
```

**Verification:**
```python
assert {i.name for i in self.get_function_roots(f)} == {'x', 'p', 'sigma'}
```

### Step 4: Assign x = pm.Data(...)

```python
x = pm.Data('x', np.zeros(10))
```

**Verification:**
```python
assert volatile_rvs == {category, obs}
```

### Step 5: Assign y = pm.Data(...)

```python
y = pm.Data('y', np.ones(10))
```

**Verification:**
```python
assert {i.name for i in self.get_function_inputs(f)} == {'beta', 'sigma'}
```

### Step 6: Assign category = pm.Categorical(...)

```python
category = pm.Categorical('category', p, observed=x)
```

**Verification:**
```python
assert {i.name for i in self.get_function_roots(f)} == {'x', 'p', 'beta', 'sigma'}
```

### Step 7: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 0.1, size=p.shape)
```

### Step 8: Assign mu = pm.Deterministic(...)

```python
mu = pm.Deterministic('mu', beta[category])
```

### Step 9: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', 0.1)
```

### Step 10: Assign obs = pm.Normal(...)

```python
obs = pm.Normal('obs', mu, sigma, observed=y, shape=mu.shape)
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    p = pm.Data('p', np.array([0.25, 0.5, 0.25]))
    x = pm.Data('x', np.zeros(10))
    y = pm.Data('y', np.ones(10))
    category = pm.Categorical('category', p, observed=x)
    beta = pm.Normal('beta', 0, 0.1, size=p.shape)
    mu = pm.Deterministic('mu', beta[category])
    sigma = pm.HalfNormal('sigma', 0.1)
    obs = pm.Normal('obs', mu, sigma, observed=y, shape=mu.shape)
f, volatile_rvs = compile_forward_sampling_function(outputs=model.observed_RVs, vars_in_trace=[beta, mu, sigma], basic_rvs=model.basic_RVs)
assert volatile_rvs == {category, beta, obs}
assert {i.name for i in self.get_function_inputs(f)} == {'sigma'}
assert {i.name for i in self.get_function_roots(f)} == {'x', 'p', 'sigma'}
f, volatile_rvs = compile_forward_sampling_function(outputs=model.observed_RVs, vars_in_trace=[beta, mu, sigma], constant_data={p: p.get_value()}, basic_rvs=model.basic_RVs)
assert volatile_rvs == {category, obs}
assert {i.name for i in self.get_function_inputs(f)} == {'beta', 'sigma'}
assert {i.name for i in self.get_function_roots(f)} == {'x', 'p', 'beta', 'sigma'}
```

## Next Steps


---

*Source: test_forward.py:155 | Complexity: Advanced | Last updated: 2026-05-18*