# How To: Rt Bias

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rt bias

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20111214)
```

**Verification:**
```python
assert_true(np.abs(bias) < bias_thresh)
```

### Step 2: Assign unknown = value

```python
mu, std, count = (100, 10, 100)
```

### Step 3: Assign arr = rng.normal(...)

```python
arr = rng.normal(mu, std, size=(count,))
```

### Step 4: Assign eps = value

```python
eps = np.finfo(np.float32).eps
```

### Step 5: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

### Step 6: Assign arr_t = arr.astype(...)

```python
arr_t = arr.astype(in_dt)
```

### Step 7: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr_t, aff)
```

### Step 8: Assign img_back = round_trip(...)

```python
img_back = round_trip(img)
```

### Step 9: Assign arr_back_sc = img_back.get_data(...)

```python
arr_back_sc = img_back.get_data()
```

### Step 10: Assign unknown = img_back.get_header.get_slope_inter(...)

```python
slope, inter = img_back.get_header().get_slope_inter()
```

### Step 11: Assign bias = np.mean(...)

```python
bias = np.mean(arr_t - arr_back_sc)
```

### Step 12: Assign max_miss = rt_err_estimate(...)

```python
max_miss = rt_err_estimate(arr_t, arr_back_sc.dtype, slope, inter)
```

### Step 13: Assign bias_thresh = np.max(...)

```python
bias_thresh = np.max([max_miss / np.sqrt(count), eps])
```

### Step 14: Call assert_true()

```python
assert_true(np.abs(bias) < bias_thresh)
```


## Complete Example

```python
# Workflow
rng = np.random.RandomState(20111214)
mu, std, count = (100, 10, 100)
arr = rng.normal(mu, std, size=(count,))
eps = np.finfo(np.float32).eps
aff = np.eye(4)
for in_dt in (np.float32, np.float64):
    arr_t = arr.astype(in_dt)
    for out_dt in IUINT_TYPES:
        img = Nifti1Image(arr_t, aff)
        img_back = round_trip(img)
        arr_back_sc = img_back.get_data()
        slope, inter = img_back.get_header().get_slope_inter()
        bias = np.mean(arr_t - arr_back_sc)
        max_miss = rt_err_estimate(arr_t, arr_back_sc.dtype, slope, inter)
        bias_thresh = np.max([max_miss / np.sqrt(count), eps])
        assert_true(np.abs(bias) < bias_thresh)
```

## Next Steps


---

*Source: test_nifti1.py:1000 | Complexity: Advanced | Last updated: 2026-05-18*