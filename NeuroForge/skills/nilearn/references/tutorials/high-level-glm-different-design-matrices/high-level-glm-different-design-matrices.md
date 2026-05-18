# How To: High Level Glm Different Design Matrices

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test can estimate a contrast when design matrices are different.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test can estimate a contrast when design matrices are different.'

```python
'Test can estimate a contrast when design matrices are different.'
```

**Verification:**
```python
assert z_joint.shape == (7, 8, 7)
```

### Step 2: Assign unknown = value

```python
shapes, rk = (((7, 8, 7, 15), (7, 8, 7, 19)), 3)
```

**Verification:**
```python
assert_almost_equal(get_data(z1) + get_data(z2), 2 * get_data(z_joint))
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign unknown = np.ones(...)

```python
design_matrices[1]['new'] = np.ones((19, 1))
```

### Step 5: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data, design_matrices=design_matrices)
```

### Step 6: Assign z_joint = multi_run_model.compute_contrast(...)

```python
z_joint = multi_run_model.compute_contrast([np.eye(rk)[:1], np.eye(rk + 1)[:1]], output_type='effect_size')
```

**Verification:**
```python
assert z_joint.shape == (7, 8, 7)
```

### Step 7: Assign model1 = FirstLevelModel.fit(...)

```python
model1 = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 8: Assign z1 = model1.compute_contrast(...)

```python
z1 = model1.compute_contrast(np.eye(rk)[:1], output_type='effect_size')
```

### Step 9: Assign model2 = FirstLevelModel.fit(...)

```python
model2 = FirstLevelModel(mask_img=mask).fit(fmri_data[1], design_matrices=design_matrices[1])
```

### Step 10: Assign z2 = model2.compute_contrast(...)

```python
z2 = model2.compute_contrast(np.eye(rk + 1)[:1], output_type='effect_size')
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(get_data(z1) + get_data(z2), 2 * get_data(z_joint))
```


## Complete Example

```python
# Workflow
'Test can estimate a contrast when design matrices are different.'
shapes, rk = (((7, 8, 7, 15), (7, 8, 7, 19)), 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
design_matrices[1]['new'] = np.ones((19, 1))
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data, design_matrices=design_matrices)
z_joint = multi_run_model.compute_contrast([np.eye(rk)[:1], np.eye(rk + 1)[:1]], output_type='effect_size')
assert z_joint.shape == (7, 8, 7)
model1 = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[0])
z1 = model1.compute_contrast(np.eye(rk)[:1], output_type='effect_size')
model2 = FirstLevelModel(mask_img=mask).fit(fmri_data[1], design_matrices=design_matrices[1])
z2 = model2.compute_contrast(np.eye(rk + 1)[:1], output_type='effect_size')
assert_almost_equal(get_data(z1) + get_data(z2), 2 * get_data(z_joint))
```

## Next Steps


---

*Source: test_first_level.py:433 | Complexity: Advanced | Last updated: 2026-05-18*