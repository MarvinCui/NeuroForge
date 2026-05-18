# How To: Voxel Neighbors

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test finding points above a threshold near a seed location.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test finding points above a threshold near a seed location.'

```python
'Test finding points above a threshold near a seed location.'
```

**Verification:**
```python
assert volume.difference(true_volume) == set()
```

### Step 2: Assign locs = np.array(...)

```python
locs = np.array(np.meshgrid(*[np.linspace(-1, 1, 101)] * 3))
```

**Verification:**
```python
assert true_volume.difference(volume) == set()
```

### Step 3: Assign image = value

```python
image = 1 - np.linalg.norm(locs, axis=0)
```

### Step 4: Assign true_volume = set(...)

```python
true_volume = set([tuple(coord) for coord in np.array(np.where(image > 0.95)).T])
```

### Step 5: Assign volume = _voxel_neighbors(...)

```python
volume = _voxel_neighbors(np.array([-0.3, 0.6, 0.5]) + (np.array(image.shape[0]) - 1) / 2, image, thresh=0.95, use_relative=False)
```

**Verification:**
```python
assert volume.difference(true_volume) == set()
```


## Complete Example

```python
# Workflow
'Test finding points above a threshold near a seed location.'
locs = np.array(np.meshgrid(*[np.linspace(-1, 1, 101)] * 3))
image = 1 - np.linalg.norm(locs, axis=0)
true_volume = set([tuple(coord) for coord in np.array(np.where(image > 0.95)).T])
volume = _voxel_neighbors(np.array([-0.3, 0.6, 0.5]) + (np.array(image.shape[0]) - 1) / 2, image, thresh=0.95, use_relative=False)
assert volume.difference(true_volume) == set()
assert true_volume.difference(volume) == set()
```

## Next Steps


---

*Source: test_surface.py:321 | Complexity: Intermediate | Last updated: 2026-05-18*