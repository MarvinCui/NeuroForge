# How To: High Level Glm With Data With Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test GLM can be run with mask.

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

### Step 1: 'Test GLM can be run with mask.'

```python
'Test GLM can be run with mask.'
```

**Verification:**
```python
assert_array_equal(get_data(z_image) == 0.0, get_data(mask) == 0.0)
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 5)], 3)
```

**Verification:**
```python
assert (get_data(variance_image)[get_data(mask) > 0] > 0.001).all()
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
```

**Verification:**
```python
assert_array_equal(get_data(all_images['z_score']), get_data(z_image))
```

### Step 4: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data, design_matrices=design_matrices)
```

**Verification:**
```python
assert_array_equal(get_data(all_images['p_value']), get_data(p_value))
```

### Step 5: Assign z_image = multi_run_model.compute_contrast(...)

```python
z_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='z_score')
```

**Verification:**
```python
assert_array_equal(get_data(all_images['stat']), get_data(stat_image))
```

### Step 6: Assign p_value = multi_run_model.compute_contrast(...)

```python
p_value = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='p_value')
```

**Verification:**
```python
assert_array_equal(get_data(all_images['effect_size']), get_data(effect_image))
```

### Step 7: Assign stat_image = multi_run_model.compute_contrast(...)

```python
stat_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='stat')
```

**Verification:**
```python
assert_array_equal(get_data(all_images['effect_variance']), get_data(variance_image))
```

### Step 8: Assign effect_image = multi_run_model.compute_contrast(...)

```python
effect_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='effect_size')
```

### Step 9: Assign variance_image = multi_run_model.compute_contrast(...)

```python
variance_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='effect_variance')
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(get_data(z_image) == 0.0, get_data(mask) == 0.0)
```

**Verification:**
```python
assert (get_data(variance_image)[get_data(mask) > 0] > 0.001).all()
```

### Step 11: Assign all_images = multi_run_model.compute_contrast(...)

```python
all_images = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='all')
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(get_data(all_images['z_score']), get_data(z_image))
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(get_data(all_images['p_value']), get_data(p_value))
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(get_data(all_images['stat']), get_data(stat_image))
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(get_data(all_images['effect_size']), get_data(effect_image))
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(get_data(all_images['effect_variance']), get_data(variance_image))
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'Test GLM can be run with mask.'
shapes, rk = ([(*shape_3d_default, 5)], 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data, design_matrices=design_matrices)
z_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='z_score')
p_value = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='p_value')
stat_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='stat')
effect_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='effect_size')
variance_image = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='effect_variance')
assert_array_equal(get_data(z_image) == 0.0, get_data(mask) == 0.0)
assert (get_data(variance_image)[get_data(mask) > 0] > 0.001).all()
all_images = multi_run_model.compute_contrast(np.eye(rk)[:2], output_type='all')
assert_array_equal(get_data(all_images['z_score']), get_data(z_image))
assert_array_equal(get_data(all_images['p_value']), get_data(p_value))
assert_array_equal(get_data(all_images['stat']), get_data(stat_image))
assert_array_equal(get_data(all_images['effect_size']), get_data(effect_image))
assert_array_equal(get_data(all_images['effect_variance']), get_data(variance_image))
```

## Next Steps


---

*Source: test_first_level.py:318 | Complexity: Advanced | Last updated: 2026-05-18*