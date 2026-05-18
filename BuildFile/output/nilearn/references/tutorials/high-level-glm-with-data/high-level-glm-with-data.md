# How To: High Level Glm With Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: High level test of GLM.

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
# Fixtures: shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'High level test of GLM.'

```python
'High level test of GLM.'
```

**Verification:**
```python
assert np.sum(get_data(z_image) != 0) == n_voxels
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 5)], 3)
```

**Verification:**
```python
assert get_data(z_image).std() < 3.0
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
```

### Step 4: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
```

### Step 5: Assign n_voxels = get_data.sum(...)

```python
n_voxels = get_data(multi_run_model.mask_img_).sum()
```

### Step 6: Assign z_image = multi_run_model.compute_contrast(...)

```python
z_image = multi_run_model.compute_contrast(np.eye(rk)[1])
```

**Verification:**
```python
assert np.sum(get_data(z_image) != 0) == n_voxels
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'High level test of GLM.'
shapes, rk = ([(*shape_3d_default, 5)], 3)
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
n_voxels = get_data(multi_run_model.mask_img_).sum()
z_image = multi_run_model.compute_contrast(np.eye(rk)[1])
assert np.sum(get_data(z_image) != 0) == n_voxels
assert get_data(z_image).std() < 3.0
```

## Next Steps


---

*Source: test_first_level.py:270 | Complexity: Intermediate | Last updated: 2026-05-18*