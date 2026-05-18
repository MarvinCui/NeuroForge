# How To: Sample Condition 3

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the experimental condition sampling -- oversampling=10.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test the experimental condition sampling -- oversampling=10.'

```python
'Test the experimental condition sampling -- oversampling=10.'
```

**Verification:**
```python
assert_almost_equal(reg.sum(), 60.0)
```

### Step 2: Assign condition = value

```python
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
```

**Verification:**
```python
assert reg[10] == 1
```

### Step 3: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 49, 50)
```

**Verification:**
```python
assert reg[380] == 1
```

### Step 4: Assign unknown = _sample_condition(...)

```python
reg, _ = _sample_condition(condition, frame_times, oversampling=10, min_onset=0)
```

**Verification:**
```python
assert reg[210] == 1
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(reg.sum(), 60.0)
```

**Verification:**
```python
assert np.sum(reg > 0) == 60
```

### Step 6: Assign unknown = _sample_condition(...)

```python
reg_, _ = _sample_condition(condition, frame_times, oversampling=10.0, min_onset=0)
```

**Verification:**
```python
assert_almost_equal(reg, reg_)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(reg, reg_)
```


## Complete Example

```python
# Workflow
'Test the experimental condition sampling -- oversampling=10.'
condition = ([1, 20, 36.5], [2, 2, 2], [1, 1, 1])
frame_times = np.linspace(0, 49, 50)
reg, _ = _sample_condition(condition, frame_times, oversampling=10, min_onset=0)
assert_almost_equal(reg.sum(), 60.0)
assert reg[10] == 1
assert reg[380] == 1
assert reg[210] == 1
assert np.sum(reg > 0) == 60
reg_, _ = _sample_condition(condition, frame_times, oversampling=10.0, min_onset=0)
assert_almost_equal(reg, reg_)
```

## Next Steps


---

*Source: test_hemodynamic_models.py:141 | Complexity: Intermediate | Last updated: 2026-05-18*