# How To: Process Second Level Input As Dataframe

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Unit tests for function _process_second_level_input_as_dataframe().

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
# Fixtures: input_df
```

## Step-by-Step Guide

### Step 1: 'Unit tests for function _process_second_level_input_as_dataframe().'

```python
'Unit tests for function _process_second_level_input_as_dataframe().'
```

**Verification:**
```python
assert sample_map == 'foo.nii'
```

### Step 2: Assign unknown = _process_second_level_input_as_dataframe(...)

```python
sample_map, subjects_label = _process_second_level_input_as_dataframe(input_df)
```

**Verification:**
```python
assert subjects_label == ['foo', 'bar', 'baz']
```


## Complete Example

```python
# Setup
# Fixtures: input_df

# Workflow
'Unit tests for function _process_second_level_input_as_dataframe().'
sample_map, subjects_label = _process_second_level_input_as_dataframe(input_df)
assert sample_map == 'foo.nii'
assert subjects_label == ['foo', 'bar', 'baz']
```

## Next Steps


---

*Source: test_second_level.py:91 | Complexity: Beginner | Last updated: 2026-05-18*