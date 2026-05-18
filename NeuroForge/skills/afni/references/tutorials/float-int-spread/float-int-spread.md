# How To: Float Int Spread

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test float int spread

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

### Step 1: Assign powers = np.arange(...)

```python
powers = np.arange(-10, 10, 0.5)
```

**Verification:**
```python
assert_true(np.all((diff <= max_miss) | (rdiff <= 1e-05)))
```

### Step 2: Assign arr = np.concatenate(...)

```python
arr = np.concatenate((-10 ** powers, 10 ** powers))
```

### Step 3: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

### Step 4: Assign arr_t = arr.astype(...)

```python
arr_t = arr.astype(in_dt)
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr_t, aff)
```

### Step 6: Assign img_back = round_trip(...)

```python
img_back = round_trip(img)
```

### Step 7: Assign arr_back_sc = img_back.get_data(...)

```python
arr_back_sc = img_back.get_data()
```

### Step 8: Assign unknown = img_back.get_header.get_slope_inter(...)

```python
slope, inter = img_back.get_header().get_slope_inter()
```

### Step 9: Assign max_miss = rt_err_estimate(...)

```python
max_miss = rt_err_estimate(arr_t, arr_back_sc.dtype, slope, inter)
```

### Step 10: Assign diff = np.abs(...)

```python
diff = np.abs(arr_t - arr_back_sc)
```

### Step 11: Assign rdiff = value

```python
rdiff = diff / np.abs(arr_t)
```

### Step 12: Call assert_true()

```python
assert_true(np.all((diff <= max_miss) | (rdiff <= 1e-05)))
```


## Complete Example

```python
# Workflow
powers = np.arange(-10, 10, 0.5)
arr = np.concatenate((-10 ** powers, 10 ** powers))
aff = np.eye(4)
for in_dt in (np.float32, np.float64):
    arr_t = arr.astype(in_dt)
    for out_dt in IUINT_TYPES:
        img = Nifti1Image(arr_t, aff)
        img_back = round_trip(img)
        arr_back_sc = img_back.get_data()
        slope, inter = img_back.get_header().get_slope_inter()
        max_miss = rt_err_estimate(arr_t, arr_back_sc.dtype, slope, inter)
        diff = np.abs(arr_t - arr_back_sc)
        rdiff = diff / np.abs(arr_t)
        assert_true(np.all((diff <= max_miss) | (rdiff <= 1e-05)))
```

## Next Steps


---

*Source: test_nifti1.py:979 | Complexity: Advanced | Last updated: 2026-05-18*