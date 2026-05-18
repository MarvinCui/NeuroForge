# How To: Slm With Flm As Inputs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test second level reporting when inputs are first level models.

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
# Fixtures: flm, contrasts
```

## Step-by-Step Guide

### Step 1: 'Test second level reporting when inputs are first level models.'

```python
'Test second level reporting when inputs are first level models.'
```

### Step 2: Assign model = SecondLevelModel(...)

```python
model = SecondLevelModel(minimize_memory=False)
```

### Step 3: Assign Y = value

```python
Y = [flm] * 3
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * 3, columns=['intercept'])
```

### Step 5: Assign first_level_contrast = contrasts

```python
first_level_contrast = contrasts
```

### Step 6: Call model.fit()

```python
model.fit(Y, design_matrix=X)
```

### Step 7: Assign c1 = value

```python
c1 = np.eye(len(model.design_matrix_.columns))[0]
```

### Step 8: Call generate_and_check_glm_report()

```python
generate_and_check_glm_report(model, contrasts=c1, first_level_contrast=first_level_contrast, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
```


## Complete Example

```python
# Setup
# Fixtures: flm, contrasts

# Workflow
'Test second level reporting when inputs are first level models.'
model = SecondLevelModel(minimize_memory=False)
Y = [flm] * 3
X = pd.DataFrame([[1]] * 3, columns=['intercept'])
first_level_contrast = contrasts
model.fit(Y, design_matrix=X)
c1 = np.eye(len(model.design_matrix_.columns))[0]
generate_and_check_glm_report(model, contrasts=c1, first_level_contrast=first_level_contrast, extra_warnings_allowed=True, duplicate_warnings_allowed=True)
```

## Next Steps


---

*Source: test_glm_reporter.py:342 | Complexity: Advanced | Last updated: 2026-05-18*