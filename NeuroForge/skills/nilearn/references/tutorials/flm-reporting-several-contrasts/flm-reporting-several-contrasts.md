# How To: Flm Reporting Several Contrasts

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test for model report can be generated with no contrasts.

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
# Fixtures: flm, tmp_path, rk
```

## Step-by-Step Guide

### Step 1: 'Test for model report can be generated with no contrasts.'

```python
'Test for model report can be generated with no contrasts.'
```

### Step 2: Assign c0 = np.zeros(...)

```python
c0 = np.zeros((1, rk))
```

### Step 3: Assign unknown = 1

```python
c0[0][0] = 1
```

### Step 4: Assign c1 = np.zeros(...)

```python
c1 = np.zeros((1, rk))
```

### Step 5: Assign unknown = 1

```python
c1[0][1] = 1
```

### Step 6: Call generate_and_check_glm_report()

```python
generate_and_check_glm_report(model=flm, pth=tmp_path, plot_type='glass', contrasts=[c0, c1], min_distance=15, alpha=0.01, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
```


## Complete Example

```python
# Setup
# Fixtures: flm, tmp_path, rk

# Workflow
'Test for model report can be generated with no contrasts.'
c0 = np.zeros((1, rk))
c0[0][0] = 1
c1 = np.zeros((1, rk))
c1[0][1] = 1
generate_and_check_glm_report(model=flm, pth=tmp_path, plot_type='glass', contrasts=[c0, c1], min_distance=15, alpha=0.01, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
```

## Next Steps


---

*Source: test_glm_reporter.py:229 | Complexity: Intermediate | Last updated: 2026-05-18*