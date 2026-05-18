# How To: Infer Effect Maps

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that the right input is inferred.

second_level_input could for example
be a list of images
or a dataframe 'mapping' a string to an image.

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
# Fixtures: tmp_path, shape_4d_default
```

## Step-by-Step Guide

### Step 1: "Check that the right input is inferred.\n\n    second_level_input could for example\n    be a list of images\n    or a dataframe 'mapping' a string to an image.\n    "

```python
"Check that the right input is inferred.\n\n    second_level_input could for example\n    be a list of images\n    or a dataframe 'mapping' a string to an image.\n    "
```

**Verification:**
```python
assert _infer_effect_maps(second_level_input, 'a') == [fmri_files[0]]
```

### Step 2: Assign rk = 3

```python
rk = 3
```

**Verification:**
```python
assert _infer_effect_maps([fmri_files[0]], None) == [fmri_files[0]]
```

### Step 3: Assign shapes = value

```python
shapes = [SHAPE, shape_4d_default]
```

**Verification:**
```python
assert len(_infer_effect_maps(second_level_input, contrast)) == 2
```

### Step 4: Assign unknown = write_fake_fmri_data_and_design(...)

```python
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk=rk, file_path=tmp_path)
```

### Step 5: Assign second_level_input = pd.DataFrame(...)

```python
second_level_input = pd.DataFrame({'map_name': ['a', 'b'], 'effects_map_path': [fmri_files[0], 'bar']})
```

**Verification:**
```python
assert _infer_effect_maps(second_level_input, 'a') == [fmri_files[0]]
```

### Step 6: Assign contrast = value

```python
contrast = np.eye(rk)[1]
```

### Step 7: Assign second_level_input = value

```python
second_level_input = [FirstLevelModel(mask_img=mask_file)] * 2
```

**Verification:**
```python
assert len(_infer_effect_maps(second_level_input, contrast)) == 2
```

### Step 8: Call model.fit()

```python
model.fit(fmri_files[i], design_matrices=design_files[i])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, shape_4d_default

# Workflow
"Check that the right input is inferred.\n\n    second_level_input could for example\n    be a list of images\n    or a dataframe 'mapping' a string to an image.\n    "
rk = 3
shapes = [SHAPE, shape_4d_default]
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk=rk, file_path=tmp_path)
second_level_input = pd.DataFrame({'map_name': ['a', 'b'], 'effects_map_path': [fmri_files[0], 'bar']})
assert _infer_effect_maps(second_level_input, 'a') == [fmri_files[0]]
assert _infer_effect_maps([fmri_files[0]], None) == [fmri_files[0]]
contrast = np.eye(rk)[1]
second_level_input = [FirstLevelModel(mask_img=mask_file)] * 2
for i, model in enumerate(second_level_input):
    model.fit(fmri_files[i], design_matrices=design_files[i])
assert len(_infer_effect_maps(second_level_input, contrast)) == 2
```

## Next Steps


---

*Source: test_second_level.py:420 | Complexity: Advanced | Last updated: 2026-05-18*