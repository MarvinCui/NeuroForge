# How To: Dims Without Coords

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dims without coords

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `scipy.stats`
- `arviz_base`
- `pytensor.compile`
- `pymc.distributions`
- `pymc.distributions.transforms`
- `pymc.model`
- `pymc.stats.log_density`
- `tests.distributions.test_multivariate`


## Step-by-Step Guide

### Step 1: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(llike.log_likelihood['y'].values, st.norm.logpdf([[[0, 0, 0], [1, 1, 1]]]))
```

**Verification:**
```python
assert len(llike.log_likelihood['obs']) == 3
```

### Step 2: Assign x = Normal(...)

```python
x = Normal('x')
```

### Step 3: Assign y = Normal(...)

```python
y = Normal('y', x, observed=[0, 0, 0], shape=(3,), dims='obs')
```

### Step 4: Assign trace = from_dict(...)

```python
trace = from_dict({'posterior': {'x': np.array([[0, 1]])}})
```

### Step 5: Assign llike = compute_log_likelihood(...)

```python
llike = compute_log_likelihood(trace)
```


## Complete Example

```python
# Workflow
with Model() as m:
    x = Normal('x')
    y = Normal('y', x, observed=[0, 0, 0], shape=(3,), dims='obs')
    trace = from_dict({'posterior': {'x': np.array([[0, 1]])}})
    llike = compute_log_likelihood(trace)
assert len(llike.log_likelihood['obs']) == 3
np.testing.assert_allclose(llike.log_likelihood['y'].values, st.norm.logpdf([[[0, 0, 0], [1, 1, 1]]]))
```

## Next Steps


---

*Source: test_log_density.py:124 | Complexity: Intermediate | Last updated: 2026-05-18*