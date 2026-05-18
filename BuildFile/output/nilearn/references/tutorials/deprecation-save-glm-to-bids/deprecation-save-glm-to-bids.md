# How To: Deprecation Save Glm To Bids

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check deprecation about moved function.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level`
- `nilearn.interfaces.bids`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check deprecation about moved function.'

```python
'Check deprecation about moved function.'
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(7, 8, 9, 15)], 3)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=None, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 5: Assign contrasts = value

```python
contrasts = {'effects of interest': np.eye(rk)}
```

### Step 6: Assign contrast_types = value

```python
contrast_types = {'effects of interest': 'F'}
```

### Step 7: Call save_glm_to_bids()

```python
save_glm_to_bids(model=single_run_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check deprecation about moved function.'
shapes, rk = ([(7, 8, 9, 15)], 3)
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
single_run_model = FirstLevelModel(mask_img=None, minimize_memory=False).fit(fmri_data[0], design_matrices=design_matrices[0])
contrasts = {'effects of interest': np.eye(rk)}
contrast_types = {'effects of interest': 'F'}
with pytest.warns(FutureWarning, match="Please import from 'nilearn.glm' instead"):
    save_glm_to_bids(model=single_run_model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmp_path)
```

## Next Steps


---

*Source: test_glm.py:11 | Complexity: Intermediate | Last updated: 2026-05-18*