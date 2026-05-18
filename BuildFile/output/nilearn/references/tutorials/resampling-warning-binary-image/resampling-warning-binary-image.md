# How To: Resampling Warning Binary Image

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test resampling warning binary image

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
# Fixtures: affine_eye, rng, force_resample
```

## Step-by-Step Guide

### Step 1: Assign data_binary = rng.integers(...)

```python
data_binary = rng.integers(4, size=(1, 4, 4), dtype='int32')
```

**Verification:**
```python
assert sorted(np.unique(data_binary)) == [0, 1]
```

### Step 2: Assign unknown = 1

```python
data_binary[data_binary > 0] = 1
```

**Verification:**
```python
assert is_binary_niimg(img_binary)
```

### Step 3: Assign rot = rotation(...)

```python
rot = rotation(0, np.pi / 4)
```

### Step 4: Assign img_binary = Nifti1Image(...)

```python
img_binary = Nifti1Image(data_binary, affine_eye)
```

**Verification:**
```python
assert is_binary_niimg(img_binary)
```

### Step 5: Call resample_img()

```python
resample_img(img_binary, target_affine=rot, interpolation='continuous', force_resample=force_resample)
```

### Step 6: Call resample_img()

```python
resample_img(img_binary, target_affine=rot, interpolation='linear', force_resample=force_resample)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, rng, force_resample

# Workflow
data_binary = rng.integers(4, size=(1, 4, 4), dtype='int32')
data_binary[data_binary > 0] = 1
assert sorted(np.unique(data_binary)) == [0, 1]
rot = rotation(0, np.pi / 4)
img_binary = Nifti1Image(data_binary, affine_eye)
assert is_binary_niimg(img_binary)
with pytest.warns(Warning, match='Resampling binary images with'):
    resample_img(img_binary, target_affine=rot, interpolation='continuous', force_resample=force_resample)
with pytest.warns(Warning, match='Resampling binary images with'):
    resample_img(img_binary, target_affine=rot, interpolation='linear', force_resample=force_resample)
```

## Next Steps


---

*Source: test_resampling.py:424 | Complexity: Intermediate | Last updated: 2026-05-18*