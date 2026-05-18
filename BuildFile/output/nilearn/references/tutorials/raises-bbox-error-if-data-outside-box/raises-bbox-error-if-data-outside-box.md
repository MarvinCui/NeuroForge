# How To: Raises Bbox Error If Data Outside Box

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Make some cases which should raise exceptions.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `math`
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn._utils`
- `nilearn._utils.niimg`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`

**Setup Required:**
```python
# Fixtures: affine_eye, force_resample
```

## Step-by-Step Guide

### Step 1: 'Make some cases which should raise exceptions.'

```python
'Make some cases which should raise exceptions.'
```

### Step 2: Assign data = np.zeros(...)

```python
data = np.zeros([8, 9, 10])
```

### Step 3: Assign affine_offset = np.array(...)

```python
affine_offset = np.array([1, 1, 1])
```

### Step 4: Assign affine = affine_eye

```python
affine = affine_eye
```

### Step 5: Assign unknown = affine_offset

```python
affine[:3, 3] = affine_offset
```

### Step 6: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

### Step 7: Assign diag = value

```python
diag = [[-1, 1, 1, 1], [1, -1, 1, 1], [1, 1, -1, 1], [-1, -1, 1, 1], [-1, 1, -1, 1], [1, -1, -1, 1]]
```

### Step 8: Assign axis_flips = np.array(...)

```python
axis_flips = np.array(list(map(np.diag, diag)))
```

### Step 9: Assign af = axis_flips

```python
af = axis_flips
```

### Step 10: Assign rotations = np.array(...)

```python
rotations = np.array([af[0][[1, 0, 2, 3]], af[0][[2, 1, 0, 3]], af[1][[1, 0, 2, 3]], af[1][[0, 2, 1, 3]], af[2][[2, 1, 0, 3]], af[2][[0, 2, 1, 3]]])
```

### Step 11: Assign new_affines = np.concatenate(...)

```python
new_affines = np.concatenate([axis_flips, rotations])
```

### Step 12: Assign new_offset = np.array(...)

```python
new_offset = np.array([0.0, 0.0, 0.0])
```

### Step 13: Assign unknown = value

```python
new_affines[:, :3, 3] = new_offset[np.newaxis, :]
```

### Step 14: Assign exception = BoundingBoxError

```python
exception = BoundingBoxError
```

### Step 15: Assign message = 'The field of view given by the target affine does not contain any of the data'

```python
message = 'The field of view given by the target affine does not contain any of the data'
```

### Step 16: Call resample_img()

```python
resample_img(img, target_affine=new_affine, force_resample=force_resample)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, force_resample

# Workflow
'Make some cases which should raise exceptions.'
data = np.zeros([8, 9, 10])
affine_offset = np.array([1, 1, 1])
affine = affine_eye
affine[:3, 3] = affine_offset
img = Nifti1Image(data, affine)
diag = [[-1, 1, 1, 1], [1, -1, 1, 1], [1, 1, -1, 1], [-1, -1, 1, 1], [-1, 1, -1, 1], [1, -1, -1, 1]]
axis_flips = np.array(list(map(np.diag, diag)))
af = axis_flips
rotations = np.array([af[0][[1, 0, 2, 3]], af[0][[2, 1, 0, 3]], af[1][[1, 0, 2, 3]], af[1][[0, 2, 1, 3]], af[2][[2, 1, 0, 3]], af[2][[0, 2, 1, 3]]])
new_affines = np.concatenate([axis_flips, rotations])
new_offset = np.array([0.0, 0.0, 0.0])
new_affines[:, :3, 3] = new_offset[np.newaxis, :]
exception = BoundingBoxError
message = 'The field of view given by the target affine does not contain any of the data'
for new_affine in new_affines:
    with pytest.raises(exception, match=message):
        resample_img(img, target_affine=new_affine, force_resample=force_resample)
```

## Next Steps


---

*Source: test_resampling.py:593 | Complexity: Advanced | Last updated: 2026-05-18*