# How To: Design Matrix Fir Column 1 3 And 11

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test design matrix fir column 1 3 and 11

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

### Step 1: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

**Verification:**
```python
assert_array_almost_equal(X[onset + 1, 0], np.ones(3))
```

### Step 2: Assign hrf_model = 'FIR'

```python
hrf_model = 'FIR'
```

**Verification:**
```python
assert_array_almost_equal(X[onset + 3, 2], np.ones(3))
```

### Step 3: Assign unknown = design_matrix_light(...)

```python
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
```

**Verification:**
```python
assert_array_almost_equal(X[onset + 4, 11], np.ones(3))
```

### Step 4: Assign onset = unknown.astype(...)

```python
onset = events.onset[events.trial_type == 'c0'].astype(int)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X[onset + 1, 0], np.ones(3))
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X[onset + 3, 2], np.ones(3))
```

### Step 7: Assign onset = unknown.astype(...)

```python
onset = events.onset[events.trial_type == 'c2'].astype(int)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(X[onset + 4, 11], np.ones(3))
```


## Complete Example

```python
# Setup
# Fixtures: frame_times

# Workflow
events = basic_paradigm()
hrf_model = 'FIR'
X, _ = design_matrix_light(frame_times, events, hrf_model=hrf_model, drift_model='polynomial', drift_order=3, fir_delays=range(1, 5))
onset = events.onset[events.trial_type == 'c0'].astype(int)
assert_array_almost_equal(X[onset + 1, 0], np.ones(3))
assert_array_almost_equal(X[onset + 3, 2], np.ones(3))
onset = events.onset[events.trial_type == 'c2'].astype(int)
assert_array_almost_equal(X[onset + 4, 11], np.ones(3))
```

## Next Steps


---

*Source: test_design_matrix.py:250 | Complexity: Advanced | Last updated: 2026-05-18*