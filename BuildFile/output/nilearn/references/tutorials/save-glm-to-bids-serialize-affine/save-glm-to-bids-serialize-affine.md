# How To: Save Glm To Bids Serialize Affine

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that affines are turned into a serializable type.

Regression test for https://github.com/nilearn/nilearn/issues/4324.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.glm.first_level`
- `nilearn.glm.io`
- `nilearn.glm.second_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that affines are turned into a serializable type.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/4324.\n    '

```python
'Test that affines are turned into a serializable type.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/4324.\n    '
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(7, 8, 9, 15)], 3)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign target_affine = value

```python
target_affine = mask.affine
```

### Step 5: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(target_affine=target_affine, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 6: Call save_glm_to_bids()

```python
save_glm_to_bids(model=single_run_model, contrasts={'effects of interest': np.eye(rk)}, contrast_types={'effects of interest': 'F'}, out_dir=tmp_path, prefix='sub-01_ses-01_task-nback', **KWARGS)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that affines are turned into a serializable type.\n\n    Regression test for https://github.com/nilearn/nilearn/issues/4324.\n    '
shapes, rk = ([(7, 8, 9, 15)], 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
target_affine = mask.affine
single_run_model = FirstLevelModel(target_affine=target_affine, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
save_glm_to_bids(model=single_run_model, contrasts={'effects of interest': np.eye(rk)}, contrast_types={'effects of interest': 'F'}, out_dir=tmp_path, prefix='sub-01_ses-01_task-nback', **KWARGS)
```

## Next Steps


---

*Source: test_io.py:147 | Complexity: Intermediate | Last updated: 2026-05-18*