# How To: Shared Variable

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that user defined shared variables (other than RNGs) aren't copied.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.tensor.exceptions`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.model.fgraph`


## Step-by-Step Guide

### Step 1: "Test that user defined shared variables (other than RNGs) aren't copied."

```python
"Test that user defined shared variables (other than RNGs) aren't copied."
```

**Verification:**
```python
assert test.owner.inputs[2] is mu
```

### Step 2: Assign mu = shared(...)

```python
mu = shared(np.array([1, 2, 3.0]), shape=(None,), name='mu')
```

**Verification:**
```python
assert test.owner.inputs[3] is sigma
```

### Step 3: Assign sigma = shared(...)

```python
sigma = shared(np.array([1.0]), shape=(1,), name='sigma')
```

**Verification:**
```python
assert m_old.rvs_to_values[test] is obs
```

### Step 4: Assign obs = shared(...)

```python
obs = shared(np.array([1, 2, 3.0]), shape=(3,), name='obs')
```

**Verification:**
```python
assert mu_new is not mu
```

### Step 5: Assign m_new = clone_model(...)

```python
m_new = clone_model(m_old)
```

**Verification:**
```python
assert sigma_new is not sigma
```

### Step 6: Assign test_new = value

```python
test_new = m_new['test']
```

**Verification:**
```python
assert obs_new is not obs
```

### Step 7: Assign unknown = test_new.owner.op.dist_params(...)

```python
mu_new, sigma_new = test_new.owner.op.dist_params(test_new.owner)
```

**Verification:**
```python
assert mu_new.type == mu.type
```

### Step 8: Assign obs_new = value

```python
obs_new = m_new.rvs_to_values[test_new]
```

**Verification:**
```python
assert sigma_new.type == sigma.type
```

### Step 9: Assign test = pm.Normal(...)

```python
test = pm.Normal('test', mu=mu, sigma=sigma, observed=obs)
```

**Verification:**
```python
assert obs_new.type == obs.type
```


## Complete Example

```python
# Workflow
"Test that user defined shared variables (other than RNGs) aren't copied."
mu = shared(np.array([1, 2, 3.0]), shape=(None,), name='mu')
sigma = shared(np.array([1.0]), shape=(1,), name='sigma')
obs = shared(np.array([1, 2, 3.0]), shape=(3,), name='obs')
with pm.Model() as m_old:
    test = pm.Normal('test', mu=mu, sigma=sigma, observed=obs)
assert test.owner.inputs[2] is mu
assert test.owner.inputs[3] is sigma
assert m_old.rvs_to_values[test] is obs
m_new = clone_model(m_old)
test_new = m_new['test']
mu_new, sigma_new = test_new.owner.op.dist_params(test_new.owner)
obs_new = m_new.rvs_to_values[test_new]
assert mu_new is not mu
assert sigma_new is not sigma
assert obs_new is not obs
assert mu_new.type == mu.type
assert sigma_new.type == sigma.type
assert obs_new.type == obs.type
assert same_storage(mu, mu_new)
assert same_storage(sigma, sigma_new)
assert same_storage(obs, obs_new)
```

## Next Steps


---

*Source: test_fgraph.py:175 | Complexity: Advanced | Last updated: 2026-05-18*