# How To: Logcdf Transformed Argument

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logcdf transformed argument

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.scalar`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pytensor.graph.traversal`
- `pytensor.scalar.math`
- `pytensor.tensor.elemwise`


## Step-by-Step Guide

### Step 1: Assign sigma_value_log = value

```python
sigma_value_log = -1.0
```

**Verification:**
```python
assert np.isclose(observed, expected)
```

### Step 2: Assign sigma_value = np.exp(...)

```python
sigma_value = np.exp(sigma_value_log)
```

### Step 3: Assign x_value = 0.5

```python
x_value = 0.5
```

### Step 4: Assign observed = m.compile_logp(...)

```python
observed = m.compile_logp(jacobian=False)({'sigma_log__': sigma_value_log, 'x': x_value})
```

### Step 5: Assign expected = pm.logp.eval(...)

```python
expected = pm.logp(pm.TruncatedNormal.dist(0, sigma_value, lower=None, upper=1.0), x_value).eval()
```

**Verification:**
```python
assert np.isclose(observed, expected)
```

### Step 6: Assign sigma = pm.HalfFlat(...)

```python
sigma = pm.HalfFlat('sigma')
```

### Step 7: Assign x = pm.Normal(...)

```python
x = pm.Normal('x', 0, sigma)
```

### Step 8: Call pm.Potential()

```python
pm.Potential('norm_term', -logcdf(x, 1.0))
```


## Complete Example

```python
# Workflow
with pm.Model() as m:
    sigma = pm.HalfFlat('sigma')
    x = pm.Normal('x', 0, sigma)
    pm.Potential('norm_term', -logcdf(x, 1.0))
sigma_value_log = -1.0
sigma_value = np.exp(sigma_value_log)
x_value = 0.5
observed = m.compile_logp(jacobian=False)({'sigma_log__': sigma_value_log, 'x': x_value})
expected = pm.logp(pm.TruncatedNormal.dist(0, sigma_value, lower=None, upper=1.0), x_value).eval()
assert np.isclose(observed, expected)
```

## Next Steps


---

*Source: test_abstract.py:83 | Complexity: Advanced | Last updated: 2026-05-18*