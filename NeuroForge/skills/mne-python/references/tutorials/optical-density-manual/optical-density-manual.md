# How To: Optical Density Manual

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test optical density on known values.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test optical density on known values.'

```python
'Test optical density on known values.'
```

**Verification:**
```python
assert_allclose(od.get_data([4]), 0.0)
```

### Step 2: Assign test_tol = 0.01

```python
test_tol = 0.01
```

**Verification:**
```python
assert_allclose(od.get_data([5])[0, :2], [0.69, -0.4], atol=test_tol)
```

### Step 3: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname_nirx, preload=True)
```

### Step 4: Assign unknown = np.ones(...)

```python
raw._data[4] = np.ones(145)
```

### Step 5: Assign test_data = value

```python
test_data = np.tile([0.5, 1.5], 73)[:145]
```

### Step 6: Assign unknown = test_data

```python
raw._data[5] = test_data
```

### Step 7: Assign od = optical_density(...)

```python
od = optical_density(raw)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(od.get_data([4]), 0.0)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(od.get_data([5])[0, :2], [0.69, -0.4], atol=test_tol)
```


## Complete Example

```python
# Workflow
'Test optical density on known values.'
test_tol = 0.01
raw = read_raw_nirx(fname_nirx, preload=True)
raw._data[4] = np.ones(145)
test_data = np.tile([0.5, 1.5], 73)[:145]
raw._data[5] = test_data
od = optical_density(raw)
assert_allclose(od.get_data([4]), 0.0)
assert_allclose(od.get_data([5])[0, :2], [0.69, -0.4], atol=test_tol)
```

## Next Steps


---

*Source: test_optical_density.py:64 | Complexity: Advanced | Last updated: 2026-05-18*