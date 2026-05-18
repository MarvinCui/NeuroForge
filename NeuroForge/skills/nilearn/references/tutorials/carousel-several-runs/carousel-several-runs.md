# How To: Carousel Several Runs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that a carousel is present when there is more than 1 run.

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
# Fixtures: matplotlib_pyplot, contrasts
```

## Step-by-Step Guide

### Step 1: 'Check that a carousel is present when there is more than 1 run.'

```python
'Check that a carousel is present when there is more than 1 run.'
```

**Verification:**
```python
assert str(report).count('id="carousel-obj-') == len(shapes)
```

### Step 2: Assign rk = 6

```python
rk = 6
```

### Step 3: Assign shapes = value

```python
shapes = ((7, 7, 7, 5), (7, 7, 7, 10), (7, 7, 7, 15))
```

### Step 4: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
```

### Step 5: Assign contrasts = np.zeros(...)

```python
contrasts = np.zeros((1, rk))
```

### Step 6: Assign unknown = 1

```python
contrasts[0][1] = 1
```

### Step 7: Assign flm_two_runs = FirstLevelModel.fit(...)

```python
flm_two_runs = FirstLevelModel(standardize=None, minimize_memory=False).fit(fmri_data, design_matrices=design_matrices)
```

### Step 8: Assign report = generate_and_check_glm_report(...)

```python
report = generate_and_check_glm_report(flm_two_runs, contrasts=contrasts, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
```

**Verification:**
```python
assert str(report).count('id="carousel-obj-') == len(shapes)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, contrasts

# Workflow
'Check that a carousel is present when there is more than 1 run.'
rk = 6
shapes = ((7, 7, 7, 5), (7, 7, 7, 10), (7, 7, 7, 15))
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
contrasts = np.zeros((1, rk))
contrasts[0][1] = 1
flm_two_runs = FirstLevelModel(standardize=None, minimize_memory=False).fit(fmri_data, design_matrices=design_matrices)
report = generate_and_check_glm_report(flm_two_runs, contrasts=contrasts, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
assert str(report).count('id="carousel-obj-') == len(shapes)
```

## Next Steps


---

*Source: test_glm_reporter.py:570 | Complexity: Advanced | Last updated: 2026-05-18*