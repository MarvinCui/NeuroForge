# How To: Nan2Zero Range Ok

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test nan2zero range ok

## Prerequisites

**Required Modules:**
- `itertools`
- `unittest`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `casting`
- `spatialimages`
- `spm99analyze`
- `testing`
- `volumeutils`
- `scipy.io`


## Step-by-Step Guide

### Step 1: Assign img_class = value

```python
img_class = self.image_class
```

**Verification:**
```python
assert_array_equal(rt_img.get_fdata(), arr)
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24, dtype=np.float32).reshape((2, 3, 4))
```

**Verification:**
```python
assert rt_img.get_fdata()[0, 0, 0] == 0
```

### Step 3: Assign unknown = value

```python
arr[0, 0, 0] = np.nan
```

### Step 4: Assign unknown = 256

```python
arr[1, 0, 0] = 256
```

### Step 5: Assign img = img_class(...)

```python
img = img_class(arr, np.eye(4))
```

### Step 6: Assign rt_img = bytesio_round_trip(...)

```python
rt_img = bytesio_round_trip(img)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(rt_img.get_fdata(), arr)
```

### Step 8: Call img.set_data_dtype()

```python
img.set_data_dtype(np.uint8)
```

**Verification:**
```python
assert rt_img.get_fdata()[0, 0, 0] == 0
```

### Step 9: Assign rt_img = bytesio_round_trip(...)

```python
rt_img = bytesio_round_trip(img)
```


## Complete Example

```python
# Workflow
img_class = self.image_class
arr = np.arange(24, dtype=np.float32).reshape((2, 3, 4))
arr[0, 0, 0] = np.nan
arr[1, 0, 0] = 256
img = img_class(arr, np.eye(4))
rt_img = bytesio_round_trip(img)
assert_array_equal(rt_img.get_fdata(), arr)
img.set_data_dtype(np.uint8)
with np.errstate(invalid='ignore'):
    rt_img = bytesio_round_trip(img)
assert rt_img.get_fdata()[0, 0, 0] == 0
```

## Next Steps


---

*Source: test_spm99analyze.py:383 | Complexity: Advanced | Last updated: 2026-05-18*