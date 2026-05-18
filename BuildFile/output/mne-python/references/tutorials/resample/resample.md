# How To: Resample

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test resampling.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy.signal`
- `scipy.signal`
- `mne`
- `mne._fiff.pick`
- `mne.filter`
- `mne.io`
- `mne.utils`
- `mne.cuda`

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: 'Test resampling.'

```python
'Test resampling.'
```

**Verification:**
```python
assert 'neighborhood' not in log
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert 'neighborhood' in log
```

### Step 3: Assign x = rng.normal(...)

```python
x = rng.normal(0, 1, (10, 10, 10))
```

**Verification:**
```python
assert x.shape == (10, 10, 10)
```

### Step 4: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert x_rs.shape == (10, 10, 5)
```

### Step 5: Assign x_2 = x.swapaxes(...)

```python
x_2 = x.swapaxes(0, 1)
```

**Verification:**
```python
assert_array_equal(x_2_rs.swapaxes(0, 1), x_rs)
```

### Step 6: Assign x_2_rs = resample(...)

```python
x_2_rs = resample(x_2, 1, 2, npad=10, method=method)
```

**Verification:**
```python
assert_array_equal(x_3_rs.swapaxes(0, 2), x_rs)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(x_2_rs.swapaxes(0, 1), x_rs)
```

**Verification:**
```python
assert_array_equal(resample([0.0, 0.0], 2, 1), [0.0, 0.0, 0.0, 0.0])
```

### Step 8: Assign x_3 = x.swapaxes(...)

```python
x_3 = x.swapaxes(0, 2)
```

### Step 9: Assign x_3_rs = resample(...)

```python
x_3_rs = resample(x_3, 1, 2, npad=10, axis=0, method=method)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(x_3_rs.swapaxes(0, 2), x_rs)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(resample([0.0, 0.0], 2, 1), [0.0, 0.0, 0.0, 0.0])
```

### Step 12: Assign x_rs = resample(...)

```python
x_rs = resample(x, 1, 2, npad=10, method=method, verbose=True)
```

**Verification:**
```python
assert 'neighborhood' not in log
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test resampling.'
rng = np.random.RandomState(0)
x = rng.normal(0, 1, (10, 10, 10))
with catch_logging() as log:
    x_rs = resample(x, 1, 2, npad=10, method=method, verbose=True)
log = log.getvalue()
if method == 'fft':
    assert 'neighborhood' not in log
else:
    assert 'neighborhood' in log
assert x.shape == (10, 10, 10)
assert x_rs.shape == (10, 10, 5)
x_2 = x.swapaxes(0, 1)
x_2_rs = resample(x_2, 1, 2, npad=10, method=method)
assert_array_equal(x_2_rs.swapaxes(0, 1), x_rs)
x_3 = x.swapaxes(0, 2)
x_3_rs = resample(x_3, 1, 2, npad=10, axis=0, method=method)
assert_array_equal(x_3_rs.swapaxes(0, 2), x_rs)
assert_array_equal(resample([0.0, 0.0], 2, 1), [0.0, 0.0, 0.0, 0.0])
```

## Next Steps


---

*Source: test_filter.py:374 | Complexity: Advanced | Last updated: 2026-05-18*