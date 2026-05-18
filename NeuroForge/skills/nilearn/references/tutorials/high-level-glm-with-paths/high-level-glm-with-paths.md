# How To: High Level Glm With Paths

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test GLM can be run with files.

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
# Fixtures: tmp_path, shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'Test GLM can be run with files.'

```python
'Test GLM can be run with files.'
```

**Verification:**
```python
assert_array_equal(z_image.affine, load(mask_file).affine)
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 5)], 3)
```

**Verification:**
```python
assert get_data(z_image).std() < 3.0
```

### Step 3: Assign unknown = write_fake_fmri_data_and_design(...)

```python
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk, file_path=tmp_path)
```

### Step 4: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_files, design_matrices=design_files)
```

### Step 5: Assign z_image = multi_run_model.compute_contrast(...)

```python
z_image = multi_run_model.compute_contrast(np.eye(rk)[1])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(z_image.affine, load(mask_file).affine)
```

**Verification:**
```python
assert get_data(z_image).std() < 3.0
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, shape_3d_default

# Workflow
'Test GLM can be run with files.'
shapes, rk = ([(*shape_3d_default, 5)], 3)
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk, file_path=tmp_path)
multi_run_model = FirstLevelModel(mask_img=None).fit(fmri_files, design_matrices=design_files)
z_image = multi_run_model.compute_contrast(np.eye(rk)[1])
assert_array_equal(z_image.affine, load(mask_file).affine)
assert get_data(z_image).std() < 3.0
```

## Next Steps


---

*Source: test_first_level.py:396 | Complexity: Intermediate | Last updated: 2026-05-18*