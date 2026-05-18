# How To: Offset Errors

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test offset errors

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

### Step 1: Assign IC = value

```python
IC = self.image_class
```

**Verification:**
```python
assert img.header.get_data_offset() == 0
```

### Step 2: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24, dtype='f4').reshape((2, 3, 4))
```

**Verification:**
```python
assert img_rt.header.get_data_offset() == 0
```

### Step 3: Assign img = IC(...)

```python
img = IC(arr, np.eye(4))
```

**Verification:**
```python
assert img.header.get_data_offset() == 0
```

### Step 4: Assign img_rt = bytesio_round_trip(...)

```python
img_rt = bytesio_round_trip(img)
```

**Verification:**
```python
assert img_rt.header.get_data_offset() == 0
```

### Step 5: Assign fm = bytesio_filemap(...)

```python
fm = bytesio_filemap(IC)
```

### Step 6: Call img.header.set_data_offset()

```python
img.header.set_data_offset(16)
```

### Step 7: Call img.to_file_map()

```python
img.to_file_map(fm)
```


## Complete Example

```python
# Workflow
IC = self.image_class
arr = np.arange(24, dtype='f4').reshape((2, 3, 4))
img = IC(arr, np.eye(4))
assert img.header.get_data_offset() == 0
img_rt = bytesio_round_trip(img)
assert img_rt.header.get_data_offset() == 0
fm = bytesio_filemap(IC)
img.header.set_data_offset(16)
with pytest.raises(HeaderDataError):
    img.to_file_map(fm)
```

## Next Steps


---

*Source: test_nifti1.py:1197 | Complexity: Intermediate | Last updated: 2026-05-18*