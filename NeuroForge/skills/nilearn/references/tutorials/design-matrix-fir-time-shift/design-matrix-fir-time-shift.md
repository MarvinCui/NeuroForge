# How To: Design Matrix Fir Time Shift

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test design matrix fir time shift

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
# Fixtures: frame_times
```

## Step-by-Step Guide

### Step 1: Assign t_r = 1.0

```python
t_r = 1.0
```

**Verification:**
```python
assert np.all(X[ct + 1, 0] > 0.5)
```

### Step 2: Assign frame_times = value

```python
frame_times = frame_times + t_r / 2
```

### Step 3: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

### Step 4: Assign hrf_model = 'FIR'

```python
hrf_model = 'FIR'
```

### Step 5: Assign unknown = design_matrix_light(...)

```python
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
```

### Step 6: Assign ct = unknown.astype(...)

```python
ct = events.onset[events.trial_type == 'c0'].astype(int)
```

**Verification:**
```python
assert np.all(X[ct + 1, 0] > 0.5)
```


## Complete Example

```python
# Setup
# Fixtures: frame_times

# Workflow
t_r = 1.0
frame_times = frame_times + t_r / 2
events = basic_paradigm()
hrf_model = 'FIR'
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
ct = events.onset[events.trial_type == 'c0'].astype(int)
assert np.all(X[ct + 1, 0] > 0.5)
```

## Next Steps


---

*Source: test_design_matrix.py:270 | Complexity: Intermediate | Last updated: 2026-05-18*