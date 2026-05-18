# How To: Make Regressor 3

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
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
assert_array_almost_equal(np.sum(reg, 0), np.array([3, 3, 3, 3]))
```

### Step 2: Assign condition = value

```python
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
```

**Verification:**
```python
assert len(reg_names) == 4
```

### Step 3: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 138, 70)
```

**Verification:**
```python
assert_array_equal(reg, reg_)
```

### Step 4: Assign hrf_model = 'fir'

```python
hrf_model = 'fir'
```

### Step 5: Assign unknown = compute_regressor(...)

```python
reg, reg_names = compute_regressor(condition, hrf_model, frame_times, fir_delays=np.arange(4))
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(np.sum(reg, 0), np.array([3, 3, 3, 3]))
```

**Verification:**
```python
assert len(reg_names) == 4
```

### Step 7: Assign unknown = compute_regressor(...)

```python
reg_, _ = compute_regressor(condition, hrf_model, frame_times, fir_delays=np.arange(4), oversampling=50.0)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(reg, reg_)
```


## Complete Example

```python
# Workflow
'Test the generated regressor.'
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
frame_times = np.linspace(0, 138, 70)
hrf_model = 'fir'
reg, reg_names = compute_regressor(condition, hrf_model, frame_times, fir_delays=np.arange(4))
assert_array_almost_equal(np.sum(reg, 0), np.array([3, 3, 3, 3]))
assert len(reg_names) == 4
reg_, _ = compute_regressor(condition, hrf_model, frame_times, fir_delays=np.arange(4), oversampling=50.0)
assert_array_equal(reg, reg_)
```

## Next Steps


---

*Source: test_hemodynamic_models.py:390 | Complexity: Advanced | Last updated: 2026-05-18*