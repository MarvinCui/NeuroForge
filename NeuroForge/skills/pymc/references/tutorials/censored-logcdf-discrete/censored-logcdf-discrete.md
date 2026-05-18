# How To: Censored Logcdf Discrete

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test censored logcdf discrete

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.distributions.shape_utils`


## Step-by-Step Guide

### Step 1: Assign probs = value

```python
probs = [0.1, 0.2, 0.2, 0.3, 0.2]
```

### Step 2: Assign cat = pm.Categorical.dist(...)

```python
cat = pm.Categorical.dist(probs)
```

### Step 3: Assign eval_points = np.array(...)

```python
eval_points = np.array([-1, 0, 1, 2, 3, 4, 5])
```

### Step 4: Assign cdf = np.cumsum(...)

```python
cdf = np.cumsum(probs)
```

### Step 5: Assign log_cdf_base = np.log(...)

```python
log_cdf_base = np.log(cdf)
```

### Step 6: Assign expected_logcdf_uncensored = np.full_like(...)

```python
expected_logcdf_uncensored = np.full_like(eval_points, -np.inf, dtype=float)
```

### Step 7: Assign unknown = log_cdf_base

```python
expected_logcdf_uncensored[1:6] = log_cdf_base
```

### Step 8: Assign unknown = 0.0

```python
expected_logcdf_uncensored[6] = 0.0
```

### Step 9: Assign censored_cat = pm.Censored.dist(...)

```python
censored_cat = pm.Censored.dist(cat, lower=None, upper=None)
```

### Step 10: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_logcdf_uncensored)
```

### Step 11: Assign censored_cat = pm.Censored.dist(...)

```python
censored_cat = pm.Censored.dist(cat, lower=1, upper=None)
```

### Step 12: Assign expected_left = np.where(...)

```python
expected_left = np.where(eval_points < 1, -np.inf, expected_logcdf_uncensored)
```

### Step 13: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_left)
```

### Step 14: Assign censored_cat = pm.Censored.dist(...)

```python
censored_cat = pm.Censored.dist(cat, lower=None, upper=3)
```

### Step 15: Assign expected_right = np.where(...)

```python
expected_right = np.where(eval_points >= 3, 0.0, expected_logcdf_uncensored)
```

### Step 16: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_right)
```

### Step 17: Assign censored_cat = pm.Censored.dist(...)

```python
censored_cat = pm.Censored.dist(cat, lower=1, upper=3)
```

### Step 18: Assign expected_interval = np.where(...)

```python
expected_interval = np.where(eval_points < 1, -np.inf, expected_logcdf_uncensored)
```

### Step 19: Assign expected_interval = np.where(...)

```python
expected_interval = np.where(eval_points >= 3, 0.0, expected_interval)
```

### Step 20: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_interval)
```


## Complete Example

```python
# Workflow
probs = [0.1, 0.2, 0.2, 0.3, 0.2]
cat = pm.Categorical.dist(probs)
eval_points = np.array([-1, 0, 1, 2, 3, 4, 5])
cdf = np.cumsum(probs)
log_cdf_base = np.log(cdf)
expected_logcdf_uncensored = np.full_like(eval_points, -np.inf, dtype=float)
expected_logcdf_uncensored[1:6] = log_cdf_base
expected_logcdf_uncensored[6] = 0.0
censored_cat = pm.Censored.dist(cat, lower=None, upper=None)
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_logcdf_uncensored)
censored_cat = pm.Censored.dist(cat, lower=1, upper=None)
expected_left = np.where(eval_points < 1, -np.inf, expected_logcdf_uncensored)
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_left)
censored_cat = pm.Censored.dist(cat, lower=None, upper=3)
expected_right = np.where(eval_points >= 3, 0.0, expected_logcdf_uncensored)
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_right)
censored_cat = pm.Censored.dist(cat, lower=1, upper=3)
expected_interval = np.where(eval_points < 1, -np.inf, expected_logcdf_uncensored)
expected_interval = np.where(eval_points >= 3, 0.0, expected_interval)
np.testing.assert_allclose(logcdf(censored_cat, eval_points).eval(), expected_interval)
```

## Next Steps


---

*Source: test_censored.py:174 | Complexity: Advanced | Last updated: 2026-05-18*