# How To: Data Scaling

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test data scaling

## Prerequisites

**Required Modules:**
- `os`
- `struct`
- `unittest`
- `warnings`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel`
- `nibabel.affines`
- `nibabel.casting`
- `nibabel.eulerangles`
- `nibabel.nifti1`
- `nibabel.optpkg`
- `nibabel.pkg_info`
- `nibabel.spatialimages`
- `nibabel.tmpdirs`
- `freesurfer`
- `orientations`
- `testing`
- `nibabel_data`
- `test_arraywriters`
- `test_orientations`
- `io`
- `json`


## Step-by-Step Guide

### Step 1: Call super.test_data_scaling()

```python
super().test_data_scaling()
```

**Verification:**
```python
assert_array_equal(hdr.get_slope_inter(), (1, 0))
```

### Step 2: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_array_almost_equal(data, rdata)
```

### Step 3: Assign data = np.arange.reshape(...)

```python
data = np.arange(0, 3, 0.5).reshape((1, 2, 3))
```

**Verification:**
```python
assert not np.allclose(hdr.get_slope_inter(), (1, 0))
```

### Step 4: Call hdr.set_data_shape()

```python
hdr.set_data_shape(data.shape)
```

**Verification:**
```python
assert_array_almost_equal(data, rdata)
```

### Step 5: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.float32)
```

**Verification:**
```python
assert_array_equal(hdr.get_slope_inter(), (1, 0))
```

### Step 6: Assign S = BytesIO(...)

```python
S = BytesIO()
```

**Verification:**
```python
assert_array_almost_equal(np.round(data), rdata)
```

### Step 7: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, S, rescale=True)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(hdr.get_slope_inter(), (1, 0))
```

### Step 9: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data, rdata)
```

### Step 11: Call hdr.set_data_dtype()

```python
hdr.set_data_dtype(np.int8)
```

### Step 12: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(1, 0)
```

### Step 13: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, S, rescale=True)
```

**Verification:**
```python
assert not np.allclose(hdr.get_slope_inter(), (1, 0))
```

### Step 14: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(data, rdata)
```

### Step 16: Call hdr.set_slope_inter()

```python
hdr.set_slope_inter(1, 0)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(hdr.get_slope_inter(), (1, 0))
```

### Step 18: Assign rdata = hdr.data_from_fileobj(...)

```python
rdata = hdr.data_from_fileobj(S)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.round(data), rdata)
```

### Step 20: Call hdr.data_to_fileobj()

```python
hdr.data_to_fileobj(data, S, rescale=False)
```


## Complete Example

```python
# Workflow
super().test_data_scaling()
hdr = self.header_class()
data = np.arange(0, 3, 0.5).reshape((1, 2, 3))
hdr.set_data_shape(data.shape)
hdr.set_data_dtype(np.float32)
S = BytesIO()
hdr.data_to_fileobj(data, S, rescale=True)
assert_array_equal(hdr.get_slope_inter(), (1, 0))
rdata = hdr.data_from_fileobj(S)
assert_array_almost_equal(data, rdata)
hdr.set_data_dtype(np.int8)
hdr.set_slope_inter(1, 0)
hdr.data_to_fileobj(data, S, rescale=True)
assert not np.allclose(hdr.get_slope_inter(), (1, 0))
rdata = hdr.data_from_fileobj(S)
assert_array_almost_equal(data, rdata)
hdr.set_slope_inter(1, 0)
with np.errstate(invalid='ignore'):
    hdr.data_to_fileobj(data, S, rescale=False)
assert_array_equal(hdr.get_slope_inter(), (1, 0))
rdata = hdr.data_from_fileobj(S)
assert_array_almost_equal(np.round(data), rdata)
```

## Next Steps


---

*Source: test_nifti1.py:99 | Complexity: Advanced | Last updated: 2026-05-18*