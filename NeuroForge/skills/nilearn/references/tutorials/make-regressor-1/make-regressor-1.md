# How To: Make Regressor 1

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the generated regressor.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test the generated regressor.'

```python
'Test the generated regressor.'
```

**Verification:**
```python
assert_almost_equal(reg.sum(), 6, 1)
```

### Step 2: Assign condition = value

```python
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
```

**Verification:**
```python
assert reg_names[0] == 'cond'
```

### Step 3: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 69, 70)
```

### Step 4: Assign hrf_model = 'spm'

```python
hrf_model = 'spm'
```

### Step 5: Assign unknown = compute_regressor(...)

```python
reg, reg_names = compute_regressor(condition, hrf_model, frame_times)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(reg.sum(), 6, 1)
```

**Verification:**
```python
assert reg_names[0] == 'cond'
```


## Complete Example

```python
# Workflow
'Test the generated regressor.'
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
frame_times = np.linspace(0, 69, 70)
hrf_model = 'spm'
reg, reg_names = compute_regressor(condition, hrf_model, frame_times)
assert_almost_equal(reg.sum(), 6, 1)
assert reg_names[0] == 'cond'
```

## Next Steps


---

*Source: test_hemodynamic_models.py:366 | Complexity: Intermediate | Last updated: 2026-05-18*