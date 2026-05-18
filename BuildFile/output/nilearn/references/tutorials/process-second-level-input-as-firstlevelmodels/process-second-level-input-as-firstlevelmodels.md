# How To: Process Second Level Input As Firstlevelmodels

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Unit tests for function        _process_second_level_input_as_firstlevelmodels().
    

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
# Fixtures: shape_4d_default, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Unit tests for function        _process_second_level_input_as_firstlevelmodels().\n    '

```python
'Unit tests for function        _process_second_level_input_as_firstlevelmodels().\n    '
```

**Verification:**
```python
assert subjects_label == [f'sub-{i}' for i in range(n_subjects)]
```

### Step 2: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default])
```

**Verification:**
```python
assert isinstance(sample_map, Nifti1Image)
```

### Step 3: Assign list_of_flm = value

```python
list_of_flm = [FirstLevelModel(mask_img=mask, subject_label=f'sub-{i}').fit(fmri_data[0], design_matrices=design_matrices[0]) for i in range(n_subjects)]
```

**Verification:**
```python
assert sample_map.shape == shape_4d_default[:3]
```

### Step 4: Assign unknown = _process_second_level_input_as_firstlevelmodels(...)

```python
sample_map, subjects_label = _process_second_level_input_as_firstlevelmodels(list_of_flm)
```

**Verification:**
```python
assert subjects_label == [f'sub-{i}' for i in range(n_subjects)]
```


## Complete Example

```python
# Setup
# Fixtures: shape_4d_default, n_subjects

# Workflow
'Unit tests for function        _process_second_level_input_as_firstlevelmodels().\n    '
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default])
list_of_flm = [FirstLevelModel(mask_img=mask, subject_label=f'sub-{i}').fit(fmri_data[0], design_matrices=design_matrices[0]) for i in range(n_subjects)]
sample_map, subjects_label = _process_second_level_input_as_firstlevelmodels(list_of_flm)
assert subjects_label == [f'sub-{i}' for i in range(n_subjects)]
assert isinstance(sample_map, Nifti1Image)
assert sample_map.shape == shape_4d_default[:3]
```

## Next Steps


---

*Source: test_second_level.py:146 | Complexity: Intermediate | Last updated: 2026-05-18*