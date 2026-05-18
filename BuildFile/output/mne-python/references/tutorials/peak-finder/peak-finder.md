# How To: Peak Finder

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the peak detection method.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.preprocessing`


## Step-by-Step Guide

### Step 1: 'Test the peak detection method.'

```python
'Test the peak detection method.'
```

**Verification:**
```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

**Verification:**
```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

### Step 3: Assign unknown = peak_finder(...)

```python
peak_inds, peak_mags = peak_finder(rng.randn(20))
```

**Verification:**
```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

### Step 4: Call assert_equal()

```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

**Verification:**
```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

### Step 5: Call assert_equal()

```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

**Verification:**
```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

### Step 6: Assign unknown = peak_finder(...)

```python
peak_inds, peak_mags = peak_finder(np.arange(1, 2, 0.05))
```

**Verification:**
```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

### Step 7: Call assert_equal()

```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

**Verification:**
```python
assert_array_equal(peak_inds, [2, 4])
```

### Step 8: Call assert_equal()

```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

### Step 9: Assign unknown = peak_finder(...)

```python
peak_inds, peak_mags = peak_finder(np.zeros(20))
```

### Step 10: Call assert_equal()

```python
assert_equal(peak_inds.dtype, np.dtype('int64'))
```

### Step 11: Call assert_equal()

```python
assert_equal(peak_mags.dtype, np.dtype('float64'))
```

### Step 12: Assign unknown = peak_finder(...)

```python
peak_inds, peak_mags = peak_finder([0, 2, 5, 0, 6, -1])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(peak_inds, [2, 4])
```

### Step 14: Call peak_finder()

```python
peak_finder(np.arange(2, 1, 0.05))
```

### Step 15: Call peak_finder()

```python
peak_finder([])
```


## Complete Example

```python
# Workflow
'Test the peak detection method.'
rng = np.random.RandomState(42)
peak_inds, peak_mags = peak_finder(rng.randn(20))
assert_equal(peak_inds.dtype, np.dtype('int64'))
assert_equal(peak_mags.dtype, np.dtype('float64'))
with pytest.raises(ValueError):
    peak_finder(np.arange(2, 1, 0.05))
with pytest.raises(ValueError):
    peak_finder([])
peak_inds, peak_mags = peak_finder(np.arange(1, 2, 0.05))
assert_equal(peak_inds.dtype, np.dtype('int64'))
assert_equal(peak_mags.dtype, np.dtype('float64'))
peak_inds, peak_mags = peak_finder(np.zeros(20))
assert_equal(peak_inds.dtype, np.dtype('int64'))
assert_equal(peak_mags.dtype, np.dtype('float64'))
peak_inds, peak_mags = peak_finder([0, 2, 5, 0, 6, -1])
assert_array_equal(peak_inds, [2, 4])
```

## Next Steps


---

*Source: test_peak_finder.py:12 | Complexity: Advanced | Last updated: 2026-05-18*