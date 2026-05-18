# How To: Save Glm To Bids Reset Threshold Warning

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Get single warning threshold reset to None.

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
# Fixtures: tmp_path_factory
```

## Step-by-Step Guide

### Step 1: 'Get single warning threshold reset to None.'

```python
'Get single warning threshold reset to None.'
```

**Verification:**
```python
assert reset_threshold_warnings == 1
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_save_glm_results')
```

### Step 3: Assign unknown = value

```python
shapes, rk = ([(7, 8, 9, 15)], 3)
```

### Step 4: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 5: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=None, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 6: Assign contrasts = value

```python
contrasts = {'effects of interest': np.eye(rk)}
```

### Step 7: Assign contrast_types = value

```python
contrast_types = {'effects of interest': 'F'}
```

### Step 8: Call save_glm_to_bids()

```python
save_glm_to_bids(model=single_run_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmpdir, threshold=1.0)
```

### Step 9: Assign reset_threshold_warnings = len(...)

```python
reset_threshold_warnings = len([x for x in warning_list if "'threshold' was set to 'None'" in str(x)])
```

**Verification:**
```python
assert reset_threshold_warnings == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path_factory

# Workflow
'Get single warning threshold reset to None.'
tmpdir = tmp_path_factory.mktemp('test_save_glm_results')
shapes, rk = ([(7, 8, 9, 15)], 3)
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
single_run_model = FirstLevelModel(mask_img=None, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
contrasts = {'effects of interest': np.eye(rk)}
contrast_types = {'effects of interest': 'F'}
with warnings.catch_warnings(record=True) as warning_list:
    save_glm_to_bids(model=single_run_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmpdir, threshold=1.0)
    reset_threshold_warnings = len([x for x in warning_list if "'threshold' was set to 'None'" in str(x)])
    assert reset_threshold_warnings == 1
```

## Next Steps


---

*Source: test_io.py:109 | Complexity: Advanced | Last updated: 2026-05-18*