# How To: Oversampling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test oversampling

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
# Fixtures: n_frames
```

## Step-by-Step Guide

### Step 1: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

**Verification:**
```python
assert_almost_equal(X1.to_numpy(), X2.to_numpy())
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, n_frames - 1, n_frames)
```

**Verification:**
```python
assert_almost_equal(X2.to_numpy(), X3.to_numpy(), 0)
```

### Step 3: Assign X1 = make_first_level_design_matrix(...)

```python
X1 = make_first_level_design_matrix(frame_times, events, drift_model=None)
```

**Verification:**
```python
assert np.linalg.norm(X2.to_numpy() - X3.to_numpy()) / np.linalg.norm(X2.to_numpy()) > 0.0001
```

### Step 4: Assign X2 = make_first_level_design_matrix(...)

```python
X2 = make_first_level_design_matrix(frame_times, events, drift_model=None, oversampling=50)
```

**Verification:**
```python
assert_almost_equal(X4.to_numpy(), X5.to_numpy())
```

### Step 5: Assign X3 = make_first_level_design_matrix(...)

```python
X3 = make_first_level_design_matrix(frame_times, events, drift_model=None, oversampling=10)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(X1.to_numpy(), X2.to_numpy())
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(X2.to_numpy(), X3.to_numpy(), 0)
```

**Verification:**
```python
assert np.linalg.norm(X2.to_numpy() - X3.to_numpy()) / np.linalg.norm(X2.to_numpy()) > 0.0001
```

### Step 8: Assign X4 = make_first_level_design_matrix(...)

```python
X4 = make_first_level_design_matrix(frame_times, events, hrf_model='fir', drift_model=None, fir_delays=range(4), oversampling=1)
```

### Step 9: Assign X5 = make_first_level_design_matrix(...)

```python
X5 = make_first_level_design_matrix(frame_times, events, hrf_model='fir', drift_model=None, fir_delays=range(4), oversampling=10)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(X4.to_numpy(), X5.to_numpy())
```


## Complete Example

```python
# Setup
# Fixtures: n_frames

# Workflow
events = basic_paradigm()
frame_times = np.linspace(0, n_frames - 1, n_frames)
X1 = make_first_level_design_matrix(frame_times, events, drift_model=None)
X2 = make_first_level_design_matrix(frame_times, events, drift_model=None, oversampling=50)
X3 = make_first_level_design_matrix(frame_times, events, drift_model=None, oversampling=10)
assert_almost_equal(X1.to_numpy(), X2.to_numpy())
assert_almost_equal(X2.to_numpy(), X3.to_numpy(), 0)
assert np.linalg.norm(X2.to_numpy() - X3.to_numpy()) / np.linalg.norm(X2.to_numpy()) > 0.0001
X4 = make_first_level_design_matrix(frame_times, events, hrf_model='fir', drift_model=None, fir_delays=range(4), oversampling=1)
X5 = make_first_level_design_matrix(frame_times, events, hrf_model='fir', drift_model=None, fir_delays=range(4), oversampling=10)
assert_almost_equal(X4.to_numpy(), X5.to_numpy())
```

## Next Steps


---

*Source: test_design_matrix.py:355 | Complexity: Advanced | Last updated: 2026-05-18*