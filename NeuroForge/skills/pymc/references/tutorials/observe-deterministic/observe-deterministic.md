# How To: Observe Deterministic

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test observe deterministic

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

### Step 1: Assign y_censored_obs = np.array(...)

```python
y_censored_obs = np.array([0.9, 0.5, 0.3, 1, 1], dtype=config.floatX)
```

### Step 2: Assign m_new = observe(...)

```python
m_new = observe(m_old, {y_censored: y_censored_obs})
```

### Step 3: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 4: Assign y = pm.Normal.dist(...)

```python
y = pm.Normal.dist(x, shape=(5,))
```

### Step 5: Assign y_censored = pm.Deterministic(...)

```python
y_censored = pm.Deterministic('y_censored', pm.math.clip(y, -1, 1))
```

### Step 6: Assign x = pm.Normal(...)

```python
x = pm.Normal('x')
```

### Step 7: Call pm.Censored()

```python
pm.Censored('y_censored', pm.Normal.dist(x), lower=-1, upper=1, observed=y_censored_obs)
```


## Complete Example

```python
# Workflow
y_censored_obs = np.array([0.9, 0.5, 0.3, 1, 1], dtype=config.floatX)
with pm.Model() as m_old:
    x = pm.Normal('x')
    y = pm.Normal.dist(x, shape=(5,))
    y_censored = pm.Deterministic('y_censored', pm.math.clip(y, -1, 1))
m_new = observe(m_old, {y_censored: y_censored_obs})
with pm.Model() as m_ref:
    x = pm.Normal('x')
    pm.Censored('y_censored', pm.Normal.dist(x), lower=-1, upper=1, observed=y_censored_obs)
```

## Next Steps


---

*Source: test_conditioning.py:96 | Complexity: Intermediate | Last updated: 2026-05-18*