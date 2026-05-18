# How To: Compare Design Matrix To Spm

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test compare design matrix to spm

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn.glm.first_level.design_matrix`
- `_testing`

**Setup Required:**
```python
# Fixtures: block_duration, array
```

## Step-by-Step Guide

### Step 1: Assign unknown = spm_paradigm(...)

```python
events, frame_times = spm_paradigm(block_duration=block_duration)
```

**Verification:**
```python
assert ((spm_design_matrix - matrix) ** 2).sum() / (spm_design_matrix ** 2).sum() < 0.1
```

### Step 2: Assign X1 = make_first_level_design_matrix(...)

```python
X1 = make_first_level_design_matrix(frame_times, events, drift_model=None, hrf_model='spm')
```

### Step 3: Assign unknown = check_design_matrix(...)

```python
_, matrix, _ = check_design_matrix(X1)
```

### Step 4: Assign spm_design_matrix = value

```python
spm_design_matrix = DESIGN_MATRIX[array]
```

**Verification:**
```python
assert ((spm_design_matrix - matrix) ** 2).sum() / (spm_design_matrix ** 2).sum() < 0.1
```


## Complete Example

```python
# Setup
# Fixtures: block_duration, array

# Workflow
events, frame_times = spm_paradigm(block_duration=block_duration)
X1 = make_first_level_design_matrix(frame_times, events, drift_model=None, hrf_model='spm')
_, matrix, _ = check_design_matrix(X1)
spm_design_matrix = DESIGN_MATRIX[array]
assert ((spm_design_matrix - matrix) ** 2).sum() / (spm_design_matrix ** 2).sum() < 0.1
```

## Next Steps


---

*Source: test_design_matrix.py:442 | Complexity: Intermediate | Last updated: 2026-05-18*