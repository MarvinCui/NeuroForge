# How To: Masking First Level Model

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that using NiftiMasker when instantiating FirstLevelModel        doesn't raise Error when calling generate_report().
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level`
- `nilearn.maskers`
- `nilearn.reporting`
- `nilearn.reporting.tests._testing`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: contrasts
```

## Step-by-Step Guide

### Step 1: "Check that using NiftiMasker when instantiating FirstLevelModel        doesn't raise Error when calling generate_report().\n    "

```python
"Check that using NiftiMasker when instantiating FirstLevelModel        doesn't raise Error when calling generate_report().\n    "
```

### Step 2: Assign unknown = value

```python
shapes, rk = (((7, 7, 7, 5),), 3)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask_img=mask, standardize=None)
```

### Step 5: Call masker.fit()

```python
masker.fit(fmri_data)
```

### Step 6: Assign flm = FirstLevelModel.fit(...)

```python
flm = FirstLevelModel(mask_img=masker, minimize_memory=False).fit(fmri_data, design_matrices=design_matrices)
```

### Step 7: Call generate_and_check_glm_report()

```python
generate_and_check_glm_report(flm, contrasts=contrasts, plot_type='glass', min_distance=15, alpha=0.01, extra_warnings_allowed=False)
```


## Complete Example

```python
# Setup
# Fixtures: contrasts

# Workflow
"Check that using NiftiMasker when instantiating FirstLevelModel        doesn't raise Error when calling generate_report().\n    "
shapes, rk = (((7, 7, 7, 5),), 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
masker = NiftiMasker(mask_img=mask, standardize=None)
masker.fit(fmri_data)
flm = FirstLevelModel(mask_img=masker, minimize_memory=False).fit(fmri_data, design_matrices=design_matrices)
generate_and_check_glm_report(flm, contrasts=contrasts, plot_type='glass', min_distance=15, alpha=0.01, extra_warnings_allowed=False)
```

## Next Steps


---

*Source: test_glm_reporter.py:436 | Complexity: Intermediate | Last updated: 2026-05-18*