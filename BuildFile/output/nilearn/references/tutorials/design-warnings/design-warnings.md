# How To: Design Warnings

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that warnings are correctly raised     upon weird design specification.
    

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test that warnings are correctly raised     upon weird design specification.\n    '

```python
'Test that warnings are correctly raised     upon weird design specification.\n    '
```

### Step 2: Assign condition = value

```python
condition = ([-25, 20, 36.5], [0, 0, 0], [1, 1, 1])
```

### Step 3: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 69, 70)
```

### Step 4: Assign hrf_model = 'spm'

```python
hrf_model = 'spm'
```

### Step 5: Assign condition = value

```python
condition = ([-25, -25, 36.5], [0, 0, 0], [1, 1, 1])
```

### Step 6: Call warnings.simplefilter()

```python
warnings.simplefilter('always')
```

### Step 7: Call warnings.simplefilter()

```python
warnings.simplefilter('always')
```

### Step 8: Call compute_regressor()

```python
compute_regressor(condition, hrf_model, frame_times)
```

### Step 9: Call compute_regressor()

```python
compute_regressor(condition, hrf_model, frame_times)
```


## Complete Example

```python
# Workflow
'Test that warnings are correctly raised     upon weird design specification.\n    '
condition = ([-25, 20, 36.5], [0, 0, 0], [1, 1, 1])
frame_times = np.linspace(0, 69, 70)
hrf_model = 'spm'
with warnings.catch_warnings(record=True):
    warnings.simplefilter('always')
    with pytest.warns(UserWarning, match='Some stimulus onsets are earlier than -24.0'):
        compute_regressor(condition, hrf_model, frame_times)
condition = ([-25, -25, 36.5], [0, 0, 0], [1, 1, 1])
with warnings.catch_warnings(record=True):
    warnings.simplefilter('always')
    with pytest.warns(UserWarning, match='Some stimulus onsets are earlier than -24.0'):
        compute_regressor(condition, hrf_model, frame_times)
```

## Next Steps


---

*Source: test_hemodynamic_models.py:436 | Complexity: Advanced | Last updated: 2026-05-18*