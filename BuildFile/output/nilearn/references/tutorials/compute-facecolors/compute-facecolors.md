# How To: Compute Facecolors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if nilearn.plotting.surface._matplotlib_backend._compute_facecolors
returns expected values.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.surface._matplotlib_backend`
- `nilearn.surface`


## Step-by-Step Guide

### Step 1: 'Test if nilearn.plotting.surface._matplotlib_backend._compute_facecolors\n    returns expected values.\n    '

```python
'Test if nilearn.plotting.surface._matplotlib_backend._compute_facecolors\n    returns expected values.\n    '
```

**Verification:**
```python
assert bg_min < 0 or bg_max > 1
```

### Step 2: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

**Verification:**
```python
assert len(facecolors_auto_normalized) == len(mesh.faces)
```

### Step 3: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(fsaverage['pial_left'])
```

**Verification:**
```python
assert np.min(bg_map_normalized) == 0 and np.max(bg_map_normalized) == 1
```

### Step 4: Assign alpha = 'auto'

```python
alpha = 'auto'
```

**Verification:**
```python
assert len(facecolors_manually_normalized) == len(mesh.faces)
```

### Step 5: Assign bg_map = np.sign(...)

```python
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
```

**Verification:**
```python
assert np.allclose(facecolors_manually_normalized, facecolors_auto_normalized)
```

### Step 6: Assign unknown = value

```python
bg_min, bg_max = (np.min(bg_map), np.max(bg_map))
```

**Verification:**
```python
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
```

### Step 7: Assign facecolors_auto_normalized = _compute_facecolors(...)

```python
facecolors_auto_normalized = _compute_facecolors(bg_map, mesh.faces, len(mesh.coordinates), alpha)
```

**Verification:**
```python
assert len(facecolors_manually_rescaled) == len(mesh.faces)
```

### Step 8: Assign bg_map_normalized = value

```python
bg_map_normalized = (bg_map - bg_min) / (bg_max - bg_min)
```

**Verification:**
```python
assert not np.allclose(facecolors_manually_rescaled, facecolors_auto_normalized)
```

### Step 9: Assign facecolors_manually_normalized = _compute_facecolors(...)

```python
facecolors_manually_normalized = _compute_facecolors(bg_map_normalized, mesh.faces, len(mesh.coordinates), alpha)
```

**Verification:**
```python
assert len(facecolors_manually_normalized) == len(mesh.faces)
```

### Step 10: Assign bg_map_scaled = value

```python
bg_map_scaled = bg_map_normalized / 2 + 0.25
```

**Verification:**
```python
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
```

### Step 11: Assign facecolors_manually_rescaled = _compute_facecolors(...)

```python
facecolors_manually_rescaled = _compute_facecolors(bg_map_scaled, mesh.faces, len(mesh.coordinates), alpha)
```

**Verification:**
```python
assert len(facecolors_manually_rescaled) == len(mesh.faces)
```


## Complete Example

```python
# Workflow
'Test if nilearn.plotting.surface._matplotlib_backend._compute_facecolors\n    returns expected values.\n    '
fsaverage = fetch_surf_fsaverage()
mesh = load_surf_mesh(fsaverage['pial_left'])
alpha = 'auto'
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
bg_min, bg_max = (np.min(bg_map), np.max(bg_map))
assert bg_min < 0 or bg_max > 1
facecolors_auto_normalized = _compute_facecolors(bg_map, mesh.faces, len(mesh.coordinates), alpha)
assert len(facecolors_auto_normalized) == len(mesh.faces)
bg_map_normalized = (bg_map - bg_min) / (bg_max - bg_min)
assert np.min(bg_map_normalized) == 0 and np.max(bg_map_normalized) == 1
facecolors_manually_normalized = _compute_facecolors(bg_map_normalized, mesh.faces, len(mesh.coordinates), alpha)
assert len(facecolors_manually_normalized) == len(mesh.faces)
assert np.allclose(facecolors_manually_normalized, facecolors_auto_normalized)
bg_map_scaled = bg_map_normalized / 2 + 0.25
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
facecolors_manually_rescaled = _compute_facecolors(bg_map_scaled, mesh.faces, len(mesh.coordinates), alpha)
assert len(facecolors_manually_rescaled) == len(mesh.faces)
assert not np.allclose(facecolors_manually_rescaled, facecolors_auto_normalized)
```

## Next Steps


---

*Source: test_matplotlib_backend.py:111 | Complexity: Advanced | Last updated: 2026-05-18*