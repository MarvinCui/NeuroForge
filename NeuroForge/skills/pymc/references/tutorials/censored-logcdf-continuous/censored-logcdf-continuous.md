# How To: Censored Logcdf Continuous

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test censored logcdf continuous

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.distributions.shape_utils`


## Step-by-Step Guide

### Step 1: Assign norm = pm.Normal.dist(...)

```python
norm = pm.Normal.dist(0, 1)
```

### Step 2: Assign eval_points = np.array(...)

```python
eval_points = np.array([-np.inf, -2, -1, 0, 1, 2, np.inf])
```

### Step 3: Assign expected_logcdf_uncensored = sp.stats.norm.logcdf(...)

```python
expected_logcdf_uncensored = sp.stats.norm.logcdf(eval_points)
```

### Step 4: Assign match_str = 'divide by zero encountered in log|invalid value encountered in subtract'

```python
match_str = 'divide by zero encountered in log|invalid value encountered in subtract'
```

### Step 5: Assign censored_norm = pm.Censored.dist(...)

```python
censored_norm = pm.Censored.dist(norm, lower=None, upper=None)
```

### Step 6: Assign censored_eval = logcdf.eval(...)

```python
censored_eval = logcdf(censored_norm, eval_points).eval()
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(censored_eval, expected_logcdf_uncensored)
```

### Step 8: Assign censored_norm = pm.Censored.dist(...)

```python
censored_norm = pm.Censored.dist(norm, lower=-1, upper=None)
```

### Step 9: Assign expected_left = np.where(...)

```python
expected_left = np.where(eval_points < -1, -np.inf, expected_logcdf_uncensored)
```

### Step 10: Assign censored_eval = logcdf.eval(...)

```python
censored_eval = logcdf(censored_norm, eval_points).eval()
```

### Step 11: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(censored_eval, expected_left, rtol=1e-06)
```

### Step 12: Assign censored_norm = pm.Censored.dist(...)

```python
censored_norm = pm.Censored.dist(norm, lower=None, upper=1)
```

### Step 13: Assign expected_right = np.where(...)

```python
expected_right = np.where(eval_points >= 1, 0.0, expected_logcdf_uncensored)
```

### Step 14: Assign censored_eval = logcdf.eval(...)

```python
censored_eval = logcdf(censored_norm, eval_points).eval()
```

### Step 15: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(censored_eval, expected_right, rtol=1e-06)
```

### Step 16: Assign censored_norm = pm.Censored.dist(...)

```python
censored_norm = pm.Censored.dist(norm, lower=-1, upper=1)
```

### Step 17: Assign expected_interval = np.where(...)

```python
expected_interval = np.where(eval_points < -1, -np.inf, expected_logcdf_uncensored)
```

### Step 18: Assign expected_interval = np.where(...)

```python
expected_interval = np.where(eval_points >= 1, 0.0, expected_interval)
```

### Step 19: Assign censored_eval = logcdf.eval(...)

```python
censored_eval = logcdf(censored_norm, eval_points).eval()
```

### Step 20: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(censored_eval, expected_interval, rtol=1e-06)
```


## Complete Example

```python
# Workflow
norm = pm.Normal.dist(0, 1)
eval_points = np.array([-np.inf, -2, -1, 0, 1, 2, np.inf])
expected_logcdf_uncensored = sp.stats.norm.logcdf(eval_points)
match_str = 'divide by zero encountered in log|invalid value encountered in subtract'
censored_norm = pm.Censored.dist(norm, lower=None, upper=None)
censored_eval = logcdf(censored_norm, eval_points).eval()
np.testing.assert_allclose(censored_eval, expected_logcdf_uncensored)
censored_norm = pm.Censored.dist(norm, lower=-1, upper=None)
expected_left = np.where(eval_points < -1, -np.inf, expected_logcdf_uncensored)
censored_eval = logcdf(censored_norm, eval_points).eval()
np.testing.assert_allclose(censored_eval, expected_left, rtol=1e-06)
censored_norm = pm.Censored.dist(norm, lower=None, upper=1)
expected_right = np.where(eval_points >= 1, 0.0, expected_logcdf_uncensored)
censored_eval = logcdf(censored_norm, eval_points).eval()
np.testing.assert_allclose(censored_eval, expected_right, rtol=1e-06)
censored_norm = pm.Censored.dist(norm, lower=-1, upper=1)
expected_interval = np.where(eval_points < -1, -np.inf, expected_logcdf_uncensored)
expected_interval = np.where(eval_points >= 1, 0.0, expected_interval)
censored_eval = logcdf(censored_norm, eval_points).eval()
np.testing.assert_allclose(censored_eval, expected_interval, rtol=1e-06)
```

## Next Steps


---

*Source: test_censored.py:131 | Complexity: Advanced | Last updated: 2026-05-18*