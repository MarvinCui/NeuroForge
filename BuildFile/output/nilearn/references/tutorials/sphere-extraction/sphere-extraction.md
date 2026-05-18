# How To: Sphere Extraction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test sphere extraction.

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

### Step 1: 'Test sphere extraction.'

```python
'Test sphere extraction.'
```

**Verification:**
```python
assert masker.n_elements_ == 1
```

### Step 2: Assign seed = value

```python
seed = (1, 1, 1)
```

**Verification:**
```python
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
```

### Step 3: Assign data = rng.random(...)

```python
data = rng.random((3, 3, 3, 5))
```

**Verification:**
```python
assert_array_equal(s[:, 0], np.mean(data[np.logical_and(mask, get_data(mask_img))], axis=0))
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 5: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=1, standardize=None)
```

### Step 6: Call masker.fit()

```python
masker.fit()
```

**Verification:**
```python
assert masker.n_elements_ == 1
```

### Step 7: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 8: Assign mask = np.zeros(...)

```python
mask = np.zeros((3, 3, 3), dtype=bool)
```

### Step 9: Assign unknown = True

```python
mask[:, 1, 1] = True
```

### Step 10: Assign unknown = True

```python
mask[1, :, 1] = True
```

### Step 11: Assign unknown = True

```python
mask[1, 1, :] = True
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
```

### Step 13: Assign mask_img = np.zeros(...)

```python
mask_img = np.zeros((3, 3, 3))
```

### Step 14: Assign unknown = 1

```python
mask_img[1, :, :] = 1
```

### Step 15: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask_img, affine_eye)
```

### Step 16: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=1, mask_img=mask_img, standardize=None)
```

### Step 17: Call masker.fit()

```python
masker.fit()
```

### Step 18: Assign s = masker.transform(...)

```python
s = masker.transform(img)
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(s[:, 0], np.mean(data[np.logical_and(mask, get_data(mask_img))], axis=0))
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Test sphere extraction.'
seed = (1, 1, 1)
data = rng.random((3, 3, 3, 5))
img = Nifti1Image(data, affine_eye)
masker = NiftiSpheresMasker([seed], radius=1, standardize=None)
masker.fit()
assert masker.n_elements_ == 1
s = masker.transform(img)
mask = np.zeros((3, 3, 3), dtype=bool)
mask[:, 1, 1] = True
mask[1, :, 1] = True
mask[1, 1, :] = True
assert_array_equal(s[:, 0], np.mean(data[mask], axis=0))
mask_img = np.zeros((3, 3, 3))
mask_img[1, :, :] = 1
mask_img = Nifti1Image(mask_img, affine_eye)
masker = NiftiSpheresMasker([seed], radius=1, mask_img=mask_img, standardize=None)
masker.fit()
s = masker.transform(img)
assert_array_equal(s[:, 0], np.mean(data[np.logical_and(mask, get_data(mask_img))], axis=0))
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:76 | Complexity: Advanced | Last updated: 2026-05-18*