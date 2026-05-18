# How To: Int Int Scaling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test int int scaling

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
assert_array_equal(img_rt.get_fdata(), np.clip(arr, 0, 255))
```

### Step 2: Assign arr = value

```python
arr = np.array([-1, 0, 256], dtype=np.int16)[:, None, None]
```

### Step 3: Assign img = img_class(...)

```python
img = img_class(arr, np.eye(4))
```

### Step 4: Assign hdr = value

```python
hdr = img.header
```

### Step 5: Call img.set_data_dtype()

```python
img.set_data_dtype(np.uint8)
```

### Step 6: Call self._set_raw_scaling()

```python
self._set_raw_scaling(hdr, 1, 0 if hdr.has_data_intercept else None)
```

### Step 7: Assign img_rt = bytesio_round_trip(...)

```python
img_rt = bytesio_round_trip(img)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(img_rt.get_fdata(), np.clip(arr, 0, 255))
```


## Complete Example

```python
# Workflow
img_class = self.image_class
arr = np.array([-1, 0, 256], dtype=np.int16)[:, None, None]
img = img_class(arr, np.eye(4))
hdr = img.header
img.set_data_dtype(np.uint8)
self._set_raw_scaling(hdr, 1, 0 if hdr.has_data_intercept else None)
img_rt = bytesio_round_trip(img)
assert_array_equal(img_rt.get_fdata(), np.clip(arr, 0, 255))
```

## Next Steps


---

*Source: test_spm99analyze.py:309 | Complexity: Advanced | Last updated: 2026-05-18*