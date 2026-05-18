# How To: Design Matrix Scaling Fir Model

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test design matrix scaling fir model

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

### Step 1: Assign events = modulated_event_paradigm(...)

```python
events = modulated_event_paradigm()
```

**Verification:**
```python
assert_array_equal(X[idx + 1, 0], X[idx + 2, 1])
```

### Step 2: Assign hrf_model = 'FIR'

```python
hrf_model = 'FIR'
```

### Step 3: Assign unknown = design_matrix_light(...)

```python
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
```

### Step 4: Assign idx = unknown.astype(...)

```python
idx = events.onset[events.trial_type == 0].astype(int)
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(X[idx + 1, 0], X[idx + 2, 1])
```


## Complete Example

```python
# Setup
# Fixtures: frame_times

# Workflow
events = modulated_event_paradigm()
hrf_model = 'FIR'
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
idx = events.onset[events.trial_type == 0].astype(int)
assert_array_equal(X[idx + 1, 0], X[idx + 2, 1])
```

## Next Steps


---

*Source: test_design_matrix.py:306 | Complexity: Intermediate | Last updated: 2026-05-18*