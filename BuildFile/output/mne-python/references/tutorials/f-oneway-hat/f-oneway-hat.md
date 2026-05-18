# How To: F Oneway Hat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test f_oneway hat (low-variance) regularization.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `itertools`
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `mne`
- `mne.stats.parametric`

**Setup Required:**
```python
# Fixtures: sigma, method, seed
```

## Step-by-Step Guide

### Step 1: 'Test f_oneway hat (low-variance) regularization.'

```python
'Test f_oneway hat (low-variance) regularization.'
```

**Verification:**
```python
assert_allclose(f_ours, f_scipy, rtol=1e-07, atol=1e-06)
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(seed)
```

**Verification:**
```python
assert_array_less(f_reg[pos], f_unreg[pos])
```

### Step 3: Assign X1 = rng.standard_normal(...)

```python
X1 = rng.standard_normal(size=(10, 50))
```

### Step 4: Assign X2 = rng.standard_normal(...)

```python
X2 = rng.standard_normal(size=(10, 50))
```

### Step 5: Assign f_ours = f_oneway(...)

```python
f_ours = f_oneway(X1, X2, sigma=0.0, method=method)
```

### Step 6: Assign f_scipy = value

```python
f_scipy = scipy.stats.f_oneway(X1, X2)[0]
```

### Step 7: Call assert_allclose()

```python
assert_allclose(f_ours, f_scipy, rtol=1e-07, atol=1e-06)
```

### Step 8: Assign f_reg = f_oneway(...)

```python
f_reg = f_oneway(X1, X2, sigma=sigma, method=method)
```

### Step 9: Assign f_unreg = f_oneway(...)

```python
f_unreg = f_oneway(X1, X2, sigma=0.0)
```

### Step 10: Assign pos = value

```python
pos = f_unreg > 0
```

### Step 11: Call assert_array_less()

```python
assert_array_less(f_reg[pos], f_unreg[pos])
```


## Complete Example

```python
# Setup
# Fixtures: sigma, method, seed

# Workflow
'Test f_oneway hat (low-variance) regularization.'
rng = np.random.default_rng(seed)
X1 = rng.standard_normal(size=(10, 50))
X2 = rng.standard_normal(size=(10, 50))
f_ours = f_oneway(X1, X2, sigma=0.0, method=method)
f_scipy = scipy.stats.f_oneway(X1, X2)[0]
assert_allclose(f_ours, f_scipy, rtol=1e-07, atol=1e-06)
if sigma > 0:
    f_reg = f_oneway(X1, X2, sigma=sigma, method=method)
    f_unreg = f_oneway(X1, X2, sigma=0.0)
    pos = f_unreg > 0
    assert_array_less(f_reg[pos], f_unreg[pos])
```

## Next Steps


---

*Source: test_parametric.py:183 | Complexity: Advanced | Last updated: 2026-05-18*