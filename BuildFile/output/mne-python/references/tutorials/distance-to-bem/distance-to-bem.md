# How To: Distance To Bem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test distance_to_bem.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `copy`
- `os`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`
- `h5py`

**Setup Required:**
```python
# Fixtures: bem_type, n_pos
```

## Step-by-Step Guide

### Step 1: 'Test distance_to_bem.'

```python
'Test distance_to_bem.'
```

**Verification:**
```python
assert isinstance(dist, float)
```

### Step 2: Assign pos = np.array(...)

```python
pos = np.array([[0.0, 0.0, 0.0], [r, 0.0, 0.0], [-r, 0.0, 0.0], [0.0, r, 0.0], [0.0, -r, 0.0], [0.0, 0.0, r], [-r / np.sqrt(2.0), r / np.sqrt(2.0), 0.0], [-r / np.sqrt(2.0), -r / np.sqrt(2.0), 0.0], [0, -r / np.sqrt(2.0), r / np.sqrt(2.0)], [r / np.sqrt(3.0), r / np.sqrt(3.0), r / np.sqrt(3.0)]])
```

**Verification:**
```python
assert isinstance(dist, np.ndarray)
```

### Step 3: Assign dist = distance_to_bem(...)

```python
dist = distance_to_bem(pos, bem)
```

**Verification:**
```python
assert_allclose(dist, true_dist, rtol=1e-06, atol=1e-06)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(dist, true_dist, rtol=1e-06, atol=1e-06)
```

### Step 5: Assign bem = make_sphere_model(...)

```python
bem = make_sphere_model(r0=np.array([0, 0, 0]), verbose=0)
```

### Step 6: Assign r = value

```python
r = bem['layers'][0]['rad']
```

### Step 7: Assign true_dist = np.array(...)

```python
true_dist = np.array([r, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0])
```

### Step 8: Assign bem = read_bem_solution(...)

```python
bem = read_bem_solution(fname_bem_sol_1)
```

### Step 9: Assign r = 0.05

```python
r = 0.05
```

### Step 10: Assign true_dist = np.array(...)

```python
true_dist = np.array([0.01708097, 0.00256595, 0.01022884, 0.02306622, 0.02927288, 0.04491787, 0.00990493, 0.02244751, 0.04819345, 0.01928304])
```

### Step 11: Assign pos = value

```python
pos = pos[0, :]
```

### Step 12: Assign true_dist = value

```python
true_dist = true_dist[0]
```

**Verification:**
```python
assert isinstance(dist, float)
```


## Complete Example

```python
# Setup
# Fixtures: bem_type, n_pos

# Workflow
'Test distance_to_bem.'
if bem_type == 'sphere':
    bem = make_sphere_model(r0=np.array([0, 0, 0]), verbose=0)
    r = bem['layers'][0]['rad']
    true_dist = np.array([r, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0])
else:
    bem = read_bem_solution(fname_bem_sol_1)
    r = 0.05
    true_dist = np.array([0.01708097, 0.00256595, 0.01022884, 0.02306622, 0.02927288, 0.04491787, 0.00990493, 0.02244751, 0.04819345, 0.01928304])
pos = np.array([[0.0, 0.0, 0.0], [r, 0.0, 0.0], [-r, 0.0, 0.0], [0.0, r, 0.0], [0.0, -r, 0.0], [0.0, 0.0, r], [-r / np.sqrt(2.0), r / np.sqrt(2.0), 0.0], [-r / np.sqrt(2.0), -r / np.sqrt(2.0), 0.0], [0, -r / np.sqrt(2.0), r / np.sqrt(2.0)], [r / np.sqrt(3.0), r / np.sqrt(3.0), r / np.sqrt(3.0)]])
if n_pos == 1:
    pos = pos[0, :]
    true_dist = true_dist[0]
dist = distance_to_bem(pos, bem)
if n_pos == 1:
    assert isinstance(dist, float)
else:
    assert isinstance(dist, np.ndarray)
assert_allclose(dist, true_dist, rtol=1e-06, atol=1e-06)
```

## Next Steps


---

*Source: test_bem.py:600 | Complexity: Advanced | Last updated: 2026-05-18*