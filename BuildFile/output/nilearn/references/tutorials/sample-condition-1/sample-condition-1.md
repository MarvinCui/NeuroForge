# How To: Sample Condition 1

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that the experimental condition is correctly sampled.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test that the experimental condition is correctly sampled.'

```python
'Test that the experimental condition is correctly sampled.'
```

**Verification:**
```python
assert reg.sum() == 3
```

### Step 2: Assign condition = value

```python
condition = ([1, 20, 36.5], [0, 0, 0], [1, 1, 1])
```

**Verification:**
```python
assert reg[1] == 1
```

### Step 3: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 49, 50)
```

**Verification:**
```python
assert reg[20] == 1
```

### Step 4: Assign unknown = _sample_condition(...)

```python
reg, _ = _sample_condition(condition, frame_times, oversampling=1, min_onset=0)
```

**Verification:**
```python
assert reg[37] == 1
```

### Step 5: Assign unknown = _sample_condition(...)

```python
reg, _ = _sample_condition(condition, frame_times, oversampling=1)
```

**Verification:**
```python
assert reg.sum() == 3
```


## Complete Example

```python
# Workflow
'Test that the experimental condition is correctly sampled.'
condition = ([1, 20, 36.5], [0, 0, 0], [1, 1, 1])
frame_times = np.linspace(0, 49, 50)
reg, _ = _sample_condition(condition, frame_times, oversampling=1, min_onset=0)
assert reg.sum() == 3
assert reg[1] == 1
assert reg[20] == 1
assert reg[37] == 1
reg, _ = _sample_condition(condition, frame_times, oversampling=1)
assert reg.sum() == 3
assert reg[25] == 1
assert reg[44] == 1
assert reg[61] == 1
```

## Next Steps


---

*Source: test_hemodynamic_models.py:104 | Complexity: Intermediate | Last updated: 2026-05-18*