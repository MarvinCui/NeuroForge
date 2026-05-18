# How To: Anisotropic Sphere Extraction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test non anisotropic sphere extraction.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test non anisotropic sphere extraction.'

```python
'Test non anisotropic sphere extraction.'
```

**Verification:**
```python
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
```

### Step 2: Assign seed = value

```python
seed = (2, 1, 2)
```

**Verification:**
```python
assert_array_equal(s[:, 0], data[1, 0, 1])
```

### Step 3: Assign data = rng.random(...)

```python
data = rng.random((3, 3, 3, 5))
```

### Step 4: Assign affine = affine_eye

```python
affine = affine_eye
```

### Step 5: Assign unknown = 2

```python
affine[0, 0] = 2
```

### Step 6: Assign unknown = 2

```python
affine[2, 2] = 2
```

### Step 7: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 8: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=1, standardize=None)
```

### Step 9: Call masker.fit()

```python
masker.fit()
```

### Step 10: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 11: Assign mask = np.zeros(...)

```python
mask = np.zeros((3, 3, 3), dtype=bool)
```

### Step 12: Assign unknown = True

```python
mask[1, :, 1] = True
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
```

### Step 14: Assign mask_img = np.zeros(...)

```python
mask_img = np.zeros((3, 2, 3))
```

### Step 15: Assign unknown = 1

```python
mask_img[1, 0, 1] = 1
```

### Step 16: Assign affine_2 = affine_eye.copy(...)

```python
affine_2 = affine_eye.copy()
```

### Step 17: Assign unknown = 4

```python
affine_2[0, 0] = 4
```

### Step 18: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img, affine=affine_2)
```

### Step 19: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=1, mask_img=mask_img, standardize=None)
```

### Step 20: Call masker.fit()

```python
masker.fit()
```

### Step 21: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(s[:, 0], data[1, 0, 1])
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Test non anisotropic sphere extraction.'
seed = (2, 1, 2)
data = rng.random((3, 3, 3, 5))
affine = affine_eye
affine[0, 0] = 2
affine[2, 2] = 2
img = Nifti1Image(data, affine_eye)
masker = NiftiSpheresMasker([seed], radius=1, standardize=None)
masker.fit()
s = masker.transform(img)
mask = np.zeros((3, 3, 3), dtype=bool)
mask[1, :, 1] = True
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
mask_img = np.zeros((3, 2, 3))
mask_img[1, 0, 1] = 1
affine_2 = affine_eye.copy()
affine_2[0, 0] = 4
mask_img = Nifti1Image(mask_img, affine=affine_2)
masker = NiftiSpheresMasker([seed], radius=1, mask_img=mask_img, standardize=None)
masker.fit()
s = masker.transform(img)
assert_array_equal(s[:, 0], data[1, 0, 1])
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:117 | Complexity: Advanced | Last updated: 2026-05-18*