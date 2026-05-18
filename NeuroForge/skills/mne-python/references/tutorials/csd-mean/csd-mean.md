# How To: Csd Mean

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test averaging frequency bins of CrossSpectralDensity.

## Prerequisites

**Required Modules:**
- `pickle`
- `itertools`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne.channels`
- `mne.proj`
- `mne.time_frequency`
- `mne.time_frequency.csd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test averaging frequency bins of CrossSpectralDensity.'

```python
'Test averaging frequency bins of CrossSpectralDensity.'
```

**Verification:**
```python
assert_array_equal(csd.mean()._data, avg)
```

### Step 2: Assign csd = _make_csd(...)

```python
csd = _make_csd()
```

**Verification:**
```python
assert_array_equal(csd.mean(fmin=None, fmax=4)._data, avg)
```

### Step 3: Assign avg = value

```python
avg = [[9], [10], [11], [12], [13], [14]]
```

**Verification:**
```python
assert_array_equal(csd.mean(fmin=1, fmax=None)._data, avg)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(csd.mean()._data, avg)
```

**Verification:**
```python
assert_array_equal(csd.mean(fmin=0, fmax=None)._data, avg)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(csd.mean(fmin=None, fmax=4)._data, avg)
```

**Verification:**
```python
assert_array_equal(csd.mean(fmin=1, fmax=4)._data, avg)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(csd.mean(fmin=1, fmax=None)._data, avg)
```

**Verification:**
```python
assert_array_equal(csd_binned._data, [[3, 15], [4, 16], [5, 17], [6, 18], [7, 19], [8, 20]])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(csd.mean(fmin=0, fmax=None)._data, avg)
```

**Verification:**
```python
assert_array_equal(csd_binned._data, [[0, 15], [1, 16], [2, 17], [3, 18], [4, 19], [5, 20]])
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(csd.mean(fmin=1, fmax=4)._data, avg)
```

**Verification:**
```python
assert csd.mean()._is_sum
```

### Step 9: Assign csd_binned = csd.mean(...)

```python
csd_binned = csd.mean(fmin=[1, 3], fmax=[2, 4])
```

**Verification:**
```python
assert csd.mean().frequencies == [[1, 2, 3, 4]]
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(csd_binned._data, [[3, 15], [4, 16], [5, 17], [6, 18], [7, 19], [8, 20]])
```

**Verification:**
```python
assert csd.mean(fmin=[1, 3], fmax=[2, 4]).frequencies == [[1, 2], [3, 4]]
```

### Step 11: Assign csd_binned = csd.mean(...)

```python
csd_binned = csd.mean(fmin=[1, 3], fmax=[1, 4])
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(csd_binned._data, [[0, 15], [1, 16], [2, 17], [3, 18], [4, 19], [5, 20]])
```

**Verification:**
```python
assert csd.mean()._is_sum
```

### Step 13: Call raises()

```python
raises(ValueError, csd.mean, fmin=1, fmax=[2, 3])
```

### Step 14: Call raises()

```python
raises(ValueError, csd.mean, fmin=[1, 2], fmax=[3])
```

### Step 15: Call raises()

```python
raises(ValueError, csd.mean, fmin=[1, 2], fmax=[1, 1])
```

### Step 16: Call raises()

```python
raises(RuntimeError, csd.mean().mean)
```


## Complete Example

```python
# Workflow
'Test averaging frequency bins of CrossSpectralDensity.'
csd = _make_csd()
avg = [[9], [10], [11], [12], [13], [14]]
assert_array_equal(csd.mean()._data, avg)
assert_array_equal(csd.mean(fmin=None, fmax=4)._data, avg)
assert_array_equal(csd.mean(fmin=1, fmax=None)._data, avg)
assert_array_equal(csd.mean(fmin=0, fmax=None)._data, avg)
assert_array_equal(csd.mean(fmin=1, fmax=4)._data, avg)
csd_binned = csd.mean(fmin=[1, 3], fmax=[2, 4])
assert_array_equal(csd_binned._data, [[3, 15], [4, 16], [5, 17], [6, 18], [7, 19], [8, 20]])
csd_binned = csd.mean(fmin=[1, 3], fmax=[1, 4])
assert_array_equal(csd_binned._data, [[0, 15], [1, 16], [2, 17], [3, 18], [4, 19], [5, 20]])
assert csd.mean()._is_sum
assert csd.mean().frequencies == [[1, 2, 3, 4]]
assert csd.mean(fmin=[1, 3], fmax=[2, 4]).frequencies == [[1, 2], [3, 4]]
raises(ValueError, csd.mean, fmin=1, fmax=[2, 3])
raises(ValueError, csd.mean, fmin=[1, 2], fmax=[3])
raises(ValueError, csd.mean, fmin=[1, 2], fmax=[1, 1])
raises(RuntimeError, csd.mean().mean)
```

## Next Steps


---

*Source: test_csd.py:144 | Complexity: Advanced | Last updated: 2026-05-18*