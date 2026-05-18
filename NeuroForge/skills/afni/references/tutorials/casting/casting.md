# How To: Casting

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test casting

## Prerequisites

**Required Modules:**
- `platform`
- `numpy`
- `casting`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Call assert_array_equal()

```python
assert_array_equal(float_to_int(np.float32(0), np.int16), [0])
```

**Verification:**
```python
assert_array_equal(iarr, exp_arr)
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(float_to_int(np.nan, np.int16), [0])
```

**Verification:**
```python
assert_array_equal(iarr, im_exp)
```

### Step 3: Call assert_raises()

```python
assert_raises(CastingError, float_to_int, np.nan, np.int16, False)
```

**Verification:**
```python
assert_raises(CastingError, float_to_int, farr, it, False)
```

### Step 4: Assign ii = np.iinfo(...)

```python
ii = np.iinfo(it)
```

**Verification:**
```python
assert_array_equal(iarr, exp_arr)
```

### Step 5: Assign arr = value

```python
arr = [ii.min - 1, ii.max + 1, -np.inf, np.inf, np.nan, 0.2, 10.6]
```

**Verification:**
```python
assert_array_equal(nans, np.isnan(farr_orig))
```

### Step 6: Assign farr_orig = np.array(...)

```python
farr_orig = np.array(arr, dtype=ft)
```

**Verification:**
```python
assert_array_equal(farr[nans == False], farr_orig[nans == False])
```

### Step 7: Assign farr = farr_orig.copy(...)

```python
farr = farr_orig.copy()
```

**Verification:**
```python
assert_array_equal(float_to_int(np.float32(0), np.int16), [0])
```

### Step 8: Assign unknown = shared_range(...)

```python
mn, mx = shared_range(ft, it)
```

**Verification:**
```python
assert_array_equal(float_to_int(np.nan, np.int16), [0])
```

### Step 9: Assign iarr = float_to_int(...)

```python
iarr = float_to_int(farr, it)
```

**Verification:**
```python
assert_raises(CastingError, float_to_int, np.nan, np.int16, False)
```

### Step 10: Assign exp_arr = np.array(...)

```python
exp_arr = np.array([mn, mx, mn, mx, 0, 0, 11], dtype=it)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(iarr, exp_arr)
```

### Step 12: Assign iarr = float_to_int(...)

```python
iarr = float_to_int(farr, it, infmax=True)
```

### Step 13: Assign im_exp = np.array(...)

```python
im_exp = np.array([mn, mx, ii.min, ii.max, 0, 0, 11], dtype=it)
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(iarr, im_exp)
```

### Step 15: Call assert_raises()

```python
assert_raises(CastingError, float_to_int, farr, it, False)
```

### Step 16: Assign unknown = ft.astype(...)

```python
exp_arr[arr.index(np.nan)] = ft(np.nan).astype(it)
```

### Step 17: Assign iarr = float_to_int(...)

```python
iarr = float_to_int(farr, it, nan2zero=None)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(iarr, exp_arr)
```

### Step 19: Assign nans = np.isnan(...)

```python
nans = np.isnan(farr)
```

### Step 20: Call assert_array_equal()

```python
assert_array_equal(nans, np.isnan(farr_orig))
```

### Step 21: Call assert_array_equal()

```python
assert_array_equal(farr[nans == False], farr_orig[nans == False])
```

### Step 22: Assign mn = as_int(...)

```python
mn = as_int(mn)
```

### Step 23: Assign mx = as_int(...)

```python
mx = as_int(mx)
```

### Step 24: Assign unknown = value

```python
im_exp[0] = ii.min
```

### Step 25: Assign unknown = value

```python
im_exp[1] = ii.max
```


## Complete Example

```python
# Workflow
for ft in np.sctypes['float']:
    for it in np.sctypes['int'] + np.sctypes['uint']:
        ii = np.iinfo(it)
        arr = [ii.min - 1, ii.max + 1, -np.inf, np.inf, np.nan, 0.2, 10.6]
        farr_orig = np.array(arr, dtype=ft)
        farr = farr_orig.copy()
        mn, mx = shared_range(ft, it)
        iarr = float_to_int(farr, it)
        if ft is np.longdouble:
            mn = as_int(mn)
            mx = as_int(mx)
        exp_arr = np.array([mn, mx, mn, mx, 0, 0, 11], dtype=it)
        assert_array_equal(iarr, exp_arr)
        iarr = float_to_int(farr, it, infmax=True)
        im_exp = np.array([mn, mx, ii.min, ii.max, 0, 0, 11], dtype=it)
        if farr[0] == -np.inf:
            im_exp[0] = ii.min
        if farr[1] == np.inf:
            im_exp[1] = ii.max
        assert_array_equal(iarr, im_exp)
        assert_raises(CastingError, float_to_int, farr, it, False)
        exp_arr[arr.index(np.nan)] = ft(np.nan).astype(it)
        iarr = float_to_int(farr, it, nan2zero=None)
        assert_array_equal(iarr, exp_arr)
        nans = np.isnan(farr)
        assert_array_equal(nans, np.isnan(farr_orig))
        assert_array_equal(farr[nans == False], farr_orig[nans == False])
assert_array_equal(float_to_int(np.float32(0), np.int16), [0])
assert_array_equal(float_to_int(np.nan, np.int16), [0])
assert_raises(CastingError, float_to_int, np.nan, np.int16, False)
```

## Next Steps


---

*Source: test_casting.py:84 | Complexity: Advanced | Last updated: 2026-05-18*