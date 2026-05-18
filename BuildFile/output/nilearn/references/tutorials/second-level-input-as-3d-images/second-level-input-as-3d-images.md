# How To: Second Level Input As 3D Images

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test second level model with a list 3D image filenames as input.

Should act as a regression test for:
https://github.com/nilearn/nilearn/issues/3636

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`
- `conftest`

**Setup Required:**
```python
# Fixtures: rng, affine_eye, tmp_path, shape_3d_default, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Test second level model with a list 3D image filenames as input.\n\n    Should act as a regression test for:\n    https://github.com/nilearn/nilearn/issues/3636\n\n    '

```python
'Test second level model with a list 3D image filenames as input.\n\n    Should act as a regression test for:\n    https://github.com/nilearn/nilearn/issues/3636\n\n    '
```

### Step 2: Assign images = value

```python
images = []
```

### Step 3: Assign filenames = testing.write_imgs_to_path(...)

```python
filenames = testing.write_imgs_to_path(*images, file_path=tmp_path, create_files=True)
```

### Step 4: Assign second_level_input = filenames

```python
second_level_input = filenames
```

### Step 5: Assign design_matrix = pd.DataFrame(...)

```python
design_matrix = pd.DataFrame([1] * len(second_level_input), columns=['intercept'])
```

### Step 6: Assign second_level_model = SecondLevelModel(...)

```python
second_level_model = SecondLevelModel(smoothing_fwhm=8.0)
```

### Step 7: Assign second_level_model = second_level_model.fit(...)

```python
second_level_model = second_level_model.fit(second_level_input, design_matrix=design_matrix)
```

### Step 8: Assign data = rng.random(...)

```python
data = rng.random(shape_3d_default)
```

### Step 9: Call images.append()

```python
images.append(Nifti1Image(data, affine_eye))
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye, tmp_path, shape_3d_default, n_subjects

# Workflow
'Test second level model with a list 3D image filenames as input.\n\n    Should act as a regression test for:\n    https://github.com/nilearn/nilearn/issues/3636\n\n    '
images = []
for _ in range(n_subjects):
    data = rng.random(shape_3d_default)
    images.append(Nifti1Image(data, affine_eye))
filenames = testing.write_imgs_to_path(*images, file_path=tmp_path, create_files=True)
second_level_input = filenames
design_matrix = pd.DataFrame([1] * len(second_level_input), columns=['intercept'])
second_level_model = SecondLevelModel(smoothing_fwhm=8.0)
second_level_model = second_level_model.fit(second_level_input, design_matrix=design_matrix)
```

## Next Steps


---

*Source: test_second_level.py:116 | Complexity: Advanced | Last updated: 2026-05-18*