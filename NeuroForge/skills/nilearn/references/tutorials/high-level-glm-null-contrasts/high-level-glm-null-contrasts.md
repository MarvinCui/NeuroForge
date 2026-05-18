# How To: High Level Glm Null Contrasts

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test contrast computation is resilient to 0 values.

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

### Step 1: 'Test contrast computation is resilient to 0 values.'

```python
'Test contrast computation is resilient to 0 values.'
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 5), (*shape_3d_default, 6)], 3)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
```

### Step 5: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=None).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 6: Assign z1 = multi_run_model.compute_contrast(...)

```python
z1 = multi_run_model.compute_contrast([np.eye(rk)[:1], np.zeros((1, rk))], output_type='stat')
```

### Step 7: Assign z2 = single_run_model.compute_contrast(...)

```python
z2 = single_run_model.compute_contrast(np.eye(rk)[:1], output_type='stat')
```

### Step 8: Call np.testing.assert_almost_equal()

```python
np.testing.assert_almost_equal(get_data(z1), get_data(z2))
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'Test contrast computation is resilient to 0 values.'
shapes, rk = ([(*shape_3d_default, 5), (*shape_3d_default, 6)], 3)
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_data, design_matrices=design_matrices)
single_run_model = FirstLevelModel(mask_img=None).fit(fmri_data[0], design_matrices=design_matrices[0])
z1 = multi_run_model.compute_contrast([np.eye(rk)[:1], np.zeros((1, rk))], output_type='stat')
z2 = single_run_model.compute_contrast(np.eye(rk)[:1], output_type='stat')
np.testing.assert_almost_equal(get_data(z1), get_data(z2))
```

## Next Steps


---

*Source: test_first_level.py:411 | Complexity: Advanced | Last updated: 2026-05-18*