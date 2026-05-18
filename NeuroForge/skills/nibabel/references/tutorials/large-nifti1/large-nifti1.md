# How To: Large Nifti1

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test large nifti1

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

### Step 1: Assign image_shape = value

```python
image_shape = (91, 109, 91, 1200)
```

**Verification:**
```python
assert image_shape == data.shape
```

### Step 2: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(np.ones(image_shape, dtype=np.float32), affine=np.eye(4))
```

**Verification:**
```python
assert np.prod(image_shape) == n_ones
```

### Step 3: Assign n_ones = np.sum(...)

```python
n_ones = np.sum(data == 1.0)
```

**Verification:**
```python
assert np.prod(image_shape) == n_ones
```

### Step 4: Call img.to_filename()

```python
img.to_filename('test.nii.gz')
```

### Step 5: Assign data = load.get_fdata(...)

```python
data = load('test.nii.gz').get_fdata()
```


## Complete Example

```python
# Workflow
image_shape = (91, 109, 91, 1200)
img = Nifti1Image(np.ones(image_shape, dtype=np.float32), affine=np.eye(4))
with InTemporaryDirectory():
    img.to_filename('test.nii.gz')
    del img
    data = load('test.nii.gz').get_fdata()
assert image_shape == data.shape
n_ones = np.sum(data == 1.0)
assert np.prod(image_shape) == n_ones
```

## Next Steps


---

*Source: test_nifti1.py:1609 | Complexity: Intermediate | Last updated: 2026-05-18*