# How To: Smooth Img Scalar Array

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Ensure that fwhm=1 and fwhm=[1, 1, 1] give same result.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `re`
- `warnings`
- `collections.abc`
- `pathlib`
- `joblib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nibabel.freesurfer`
- `numpy.testing`
- `nilearn`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image.image`
- `nilearn.image.resampling`
- `nilearn.image.tests._testing`
- `nilearn.surface.surface`
- `nilearn.surface.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: affine_eye, fwhm
```

## Step-by-Step Guide

### Step 1: 'Ensure that fwhm=1 and fwhm=[1, 1, 1] give same result.'

```python
'Ensure that fwhm=1 and fwhm=[1, 1, 1] give same result.'
```

**Verification:**
```python
assert_array_equal(get_data(o1), get_data(o2))
```

### Step 2: Assign data1 = np.zeros(...)

```python
data1 = np.zeros((10, 11, 12))
```

### Step 3: Assign unknown = 1

```python
data1[2:4, 1:5, 3:6] = 1
```

### Step 4: Assign img1_nifti2 = Nifti2Image(...)

```python
img1_nifti2 = Nifti2Image(data1, affine=affine_eye)
```

### Step 5: Assign data2 = np.zeros(...)

```python
data2 = np.zeros((13, 14, 15))
```

### Step 6: Assign unknown = 9

```python
data2[2:4, 1:5, 3:6] = 9
```

### Step 7: Assign img2_nifti2 = Nifti2Image(...)

```python
img2_nifti2 = Nifti2Image(data2, affine=affine_eye)
```

### Step 8: Assign out1 = smooth_img(...)

```python
out1 = smooth_img([img1_nifti2, img2_nifti2], fwhm=1.0)
```

### Step 9: Assign out2 = smooth_img(...)

```python
out2 = smooth_img([img1_nifti2, img2_nifti2], fwhm=fwhm)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(get_data(o1), get_data(o2))
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, fwhm

# Workflow
'Ensure that fwhm=1 and fwhm=[1, 1, 1] give same result.'
data1 = np.zeros((10, 11, 12))
data1[2:4, 1:5, 3:6] = 1
img1_nifti2 = Nifti2Image(data1, affine=affine_eye)
data2 = np.zeros((13, 14, 15))
data2[2:4, 1:5, 3:6] = 9
img2_nifti2 = Nifti2Image(data2, affine=affine_eye)
out1 = smooth_img([img1_nifti2, img2_nifti2], fwhm=1.0)
out2 = smooth_img([img1_nifti2, img2_nifti2], fwhm=fwhm)
for o1, o2 in zip(out1, out2, strict=False):
    assert_array_equal(get_data(o1), get_data(o2))
```

## Next Steps


---

*Source: test_image.py:389 | Complexity: Advanced | Last updated: 2026-05-18*