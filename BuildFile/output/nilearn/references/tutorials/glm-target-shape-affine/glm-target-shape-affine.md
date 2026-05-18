# How To: Glm Target Shape Affine

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that target shape and affine are applied.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `string`
- `unittest.mock`
- `warnings`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.cluster`
- `sklearn.utils.estimator_checks`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.first_level.first_level`
- `nilearn.glm.regression`
- `nilearn.glm.thresholding`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: shape_3d_default, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Check that target shape and affine are applied.'

```python
'Check that target shape and affine are applied.'
```

**Verification:**
```python
assert model_1.mask_img_.shape == shape_3d_default
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 5)], 3)
```

**Verification:**
```python
assert z_image.shape == shape_3d_default
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
```

**Verification:**
```python
assert model_2.mask_img_.shape != shape_3d_default
```

### Step 4: Assign model_1 = FirstLevelModel.fit(...)

```python
model_1 = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
```

**Verification:**
```python
assert model_2.mask_img_.shape == (10, 11, 12)
```

### Step 5: Assign z_image = model_1.compute_contrast(...)

```python
z_image = model_1.compute_contrast(np.eye(rk)[1])
```

**Verification:**
```python
assert z_image.shape != shape_3d_default
```

### Step 6: Assign model_2 = FirstLevelModel.fit(...)

```python
model_2 = FirstLevelModel(mask_img=None, target_shape=(10, 11, 12), target_affine=affine_eye).fit(fmri_data, design_matrices=design_matrices)
```

**Verification:**
```python
assert z_image.shape == (10, 11, 12)
```

### Step 7: Assign z_image = model_2.compute_contrast(...)

```python
z_image = model_2.compute_contrast(np.eye(rk)[1])
```

**Verification:**
```python
assert z_image.shape != shape_3d_default
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default, affine_eye

# Workflow
'Check that target shape and affine are applied.'
shapes, rk = ([(*shape_3d_default, 5)], 3)
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
model_1 = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
assert model_1.mask_img_.shape == shape_3d_default
z_image = model_1.compute_contrast(np.eye(rk)[1])
assert z_image.shape == shape_3d_default
model_2 = FirstLevelModel(mask_img=None, target_shape=(10, 11, 12), target_affine=affine_eye).fit(fmri_data, design_matrices=design_matrices)
assert model_2.mask_img_.shape != shape_3d_default
assert model_2.mask_img_.shape == (10, 11, 12)
z_image = model_2.compute_contrast(np.eye(rk)[1])
assert z_image.shape != shape_3d_default
assert z_image.shape == (10, 11, 12)
```

## Next Steps


---

*Source: test_first_level.py:288 | Complexity: Intermediate | Last updated: 2026-05-18*