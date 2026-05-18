# How To: Small Radius

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check behavior when radius smaller than voxel size.

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
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Check behavior when radius smaller than voxel size.'

```python
'Check behavior when radius smaller than voxel size.'
```

### Step 2: Assign shape = value

```python
shape = (3, 3, 3)
```

### Step 3: Assign data = rng.random(...)

```python
data = rng.random(shape)
```

### Step 4: Assign mask = np.zeros(...)

```python
mask = np.zeros(shape)
```

### Step 5: Assign unknown = 1

```python
mask[1, 1, 1] = 1
```

### Step 6: Assign unknown = 1

```python
mask[2, 2, 2] = 1
```

### Step 7: Assign affine = value

```python
affine = np.eye(4) * 1.2
```

### Step 8: Assign seed = value

```python
seed = (1.4, 1.4, 1.4)
```

### Step 9: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=0.1, mask_img=Nifti1Image(mask, affine), standardize=None)
```

### Step 10: Assign spheres_data = masker.fit_transform(...)

```python
spheres_data = masker.fit_transform(Nifti1Image(data, affine))
```

### Step 11: Call masker.inverse_transform()

```python
masker.inverse_transform(spheres_data)
```

### Step 12: Assign unknown = 0

```python
mask[1, 1, 1] = 0
```

### Step 13: Assign unknown = 1

```python
mask[1, 1, 0] = 1
```

### Step 14: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=0.1, mask_img=Nifti1Image(mask, affine), standardize=None)
```

### Step 15: Call masker.fit()

```python
masker.fit(Nifti1Image(data, affine))
```

### Step 16: Assign masker = NiftiSpheresMasker(...)

```python
masker = NiftiSpheresMasker([seed], radius=1.6, mask_img=Nifti1Image(mask, affine), standardize=None)
```

### Step 17: Call masker.fit()

```python
masker.fit(Nifti1Image(data, affine))
```

### Step 18: Call masker.inverse_transform()

```python
masker.inverse_transform(spheres_data)
```

### Step 19: Call masker.fit_transform()

```python
masker.fit_transform(Nifti1Image(data, affine))
```

### Step 20: Call masker.inverse_transform()

```python
masker.inverse_transform(spheres_data)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Check behavior when radius smaller than voxel size.'
shape = (3, 3, 3)
data = rng.random(shape)
mask = np.zeros(shape)
mask[1, 1, 1] = 1
mask[2, 2, 2] = 1
affine = np.eye(4) * 1.2
seed = (1.4, 1.4, 1.4)
masker = NiftiSpheresMasker([seed], radius=0.1, mask_img=Nifti1Image(mask, affine), standardize=None)
spheres_data = masker.fit_transform(Nifti1Image(data, affine))
masker.inverse_transform(spheres_data)
mask[1, 1, 1] = 0
mask[1, 1, 0] = 1
masker = NiftiSpheresMasker([seed], radius=0.1, mask_img=Nifti1Image(mask, affine), standardize=None)
with pytest.raises(ValueError, match='These spheres are empty'):
    masker.fit_transform(Nifti1Image(data, affine))
masker.fit(Nifti1Image(data, affine))
with pytest.raises(ValueError, match='These spheres are empty'):
    masker.inverse_transform(spheres_data)
masker = NiftiSpheresMasker([seed], radius=1.6, mask_img=Nifti1Image(mask, affine), standardize=None)
masker.fit(Nifti1Image(data, affine))
masker.inverse_transform(spheres_data)
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:199 | Complexity: Advanced | Last updated: 2026-05-18*