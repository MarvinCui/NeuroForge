# How To: Observe Sum Normal

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test observe sum normal

## Prerequisites

**Required Modules:**
- `arviz`
- `numpy`
- `pytest`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph`
- `pymc`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.model.transform.conditioning`
- `pymc.model.transform.optimization`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign m_new = observe(...)

```python
m_new = observe(m_old, {y_sum: 2.0})
```

### Step 2: Assign test_point = value

```python
test_point = {'x': 0.3}
```

### Step 3: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(m_new.compile_logp()(test_point), m_ref.compile_logp()(test_point))
```

### Step 4: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 5: Assign y = pm.Normal.dist(...)

```python
y = pm.Normal.dist(mu=x, sigma=1.0, shape=(5,))
```

### Step 6: Assign y_sum = pm.Deterministic(...)

```python
y_sum = pm.Deterministic('y_sum', pm.math.sum(y))
```

### Step 7: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 8: Call pm.Normal()

```python
pm.Normal('y_sum', mu=5.0 * x, sigma=np.sqrt(5.0), observed=2.0)
```


## Complete Example

```python
# Workflow
with pm.Model() as m_old:
    x = pm.Normal('x')
    y = pm.Normal.dist(mu=x, sigma=1.0, shape=(5,))
    y_sum = pm.Deterministic('y_sum', pm.math.sum(y))
m_new = observe(m_old, {y_sum: 2.0})
with pm.Model() as m_ref:
    x = pm.Normal('x')
    pm.Normal('y_sum', mu=5.0 * x, sigma=np.sqrt(5.0), observed=2.0)
test_point = {'x': 0.3}
np.testing.assert_allclose(m_new.compile_logp()(test_point), m_ref.compile_logp()(test_point))
```

## Next Steps


---

*Source: test_conditioning.py:111 | Complexity: Advanced | Last updated: 2026-05-18*