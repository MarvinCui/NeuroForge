# How To: Censored Logp Numerical Stability

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Censored logp at 100 sigma should be finite, not -inf.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.distributions.shape_utils`

**Setup Required:**
```python
# Fixtures: censoring_side, bound_value
```

## Step-by-Step Guide

### Step 1: 'Censored logp at 100 sigma should be finite, not -inf.'

```python
'Censored logp at 100 sigma should be finite, not -inf.'
```

**Verification:**
```python
assert np.isfinite(logp_at_bound)
```

### Step 2: Assign ref_scipy = sp.stats.norm(...)

```python
ref_scipy = sp.stats.norm(0, 1)
```

**Verification:**
```python
assert np.isclose(logp_at_bound, expected_logp, rtol=1e-06)
```

### Step 3: Assign normal_dist = pm.Normal.dist(...)

```python
normal_dist = pm.Normal.dist(mu=0.0, sigma=1.0)
```

### Step 4: Assign logp_at_bound = logp.eval(...)

```python
logp_at_bound = logp(censored, bound_value).eval()
```

**Verification:**
```python
assert np.isfinite(logp_at_bound)
```

### Step 5: Assign censored = pm.Censored.dist(...)

```python
censored = pm.Censored.dist(normal_dist, lower=None, upper=bound_value)
```

### Step 6: Assign expected_logp = ref_scipy.logsf(...)

```python
expected_logp = ref_scipy.logsf(bound_value)
```

### Step 7: Assign censored = pm.Censored.dist(...)

```python
censored = pm.Censored.dist(normal_dist, lower=bound_value, upper=None)
```

### Step 8: Assign expected_logp = ref_scipy.logcdf(...)

```python
expected_logp = ref_scipy.logcdf(bound_value)
```


## Complete Example

```python
# Setup
# Fixtures: censoring_side, bound_value

# Workflow
'Censored logp at 100 sigma should be finite, not -inf.'
ref_scipy = sp.stats.norm(0, 1)
normal_dist = pm.Normal.dist(mu=0.0, sigma=1.0)
if censoring_side == 'right':
    censored = pm.Censored.dist(normal_dist, lower=None, upper=bound_value)
    expected_logp = ref_scipy.logsf(bound_value)
else:
    censored = pm.Censored.dist(normal_dist, lower=bound_value, upper=None)
    expected_logp = ref_scipy.logcdf(bound_value)
logp_at_bound = logp(censored, bound_value).eval()
assert np.isfinite(logp_at_bound)
assert np.isclose(logp_at_bound, expected_logp, rtol=1e-06)
```

## Next Steps


---

*Source: test_censored.py:224 | Complexity: Advanced | Last updated: 2026-05-18*