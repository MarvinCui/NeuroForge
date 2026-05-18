# How To: Get Vertexcolor Bg Map

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test get_vertexcolor with background map.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.surface._matplotlib_backend`
- `nilearn.surface`


## Step-by-Step Guide

### Step 1: 'Test get_vertexcolor with background map.'

```python
'Test get_vertexcolor with background map.'
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
assert len(vertexcolors_auto_normalized) == len(mesh.coordinates)
```

### Step 3: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(fsaverage['pial_left'])
```

**Verification:**
```python
assert np.min(bg_map_normalized) == 0 and np.max(bg_map_normalized) == 1
```

### Step 4: Assign surf_map = np.arange(...)

```python
surf_map = np.arange(len(mesh.coordinates))
```

**Verification:**
```python
assert len(vertexcolors_manually_normalized) == len(mesh.coordinates)
```

### Step 5: Assign colors = colorscale(...)

```python
colors = colorscale('jet', surf_map, 10)
```

**Verification:**
```python
assert vertexcolors_manually_normalized == vertexcolors_auto_normalized
```

### Step 6: Assign bg_map = np.sign(...)

```python
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
```

**Verification:**
```python
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
```

### Step 7: Assign unknown = value

```python
bg_min, bg_max = (np.min(bg_map), np.max(bg_map))
```

**Verification:**
```python
assert len(vertexcolors_manually_rescaled) == len(mesh.coordinates)
```

### Step 8: Assign vertexcolors_auto_normalized = _get_vertexcolor(...)

```python
vertexcolors_auto_normalized = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map)
```

**Verification:**
```python
assert vertexcolors_manually_rescaled != vertexcolors_auto_normalized
```

### Step 9: Assign bg_map_normalized = value

```python
bg_map_normalized = (bg_map - bg_min) / (bg_max - bg_min)
```

**Verification:**
```python
assert np.min(bg_map_normalized) == 0 and np.max(bg_map_normalized) == 1
```

### Step 10: Assign vertexcolors_manually_normalized = _get_vertexcolor(...)

```python
vertexcolors_manually_normalized = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map_normalized)
```

**Verification:**
```python
assert len(vertexcolors_manually_normalized) == len(mesh.coordinates)
```

### Step 11: Assign bg_map_scaled = value

```python
bg_map_scaled = bg_map_normalized / 2 + 0.25
```

**Verification:**
```python
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
```

### Step 12: Assign vertexcolors_manually_rescaled = _get_vertexcolor(...)

```python
vertexcolors_manually_rescaled = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map_scaled)
```

**Verification:**
```python
assert len(vertexcolors_manually_rescaled) == len(mesh.coordinates)
```


## Complete Example

```python
# Workflow
'Test get_vertexcolor with background map.'
fsaverage = fetch_surf_fsaverage()
mesh = load_surf_mesh(fsaverage['pial_left'])
surf_map = np.arange(len(mesh.coordinates))
colors = colorscale('jet', surf_map, 10)
bg_map = np.sign(load_surf_data(fsaverage['curv_left']))
bg_min, bg_max = (np.min(bg_map), np.max(bg_map))
assert bg_min < 0 or bg_max > 1
vertexcolors_auto_normalized = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map)
assert len(vertexcolors_auto_normalized) == len(mesh.coordinates)
bg_map_normalized = (bg_map - bg_min) / (bg_max - bg_min)
assert np.min(bg_map_normalized) == 0 and np.max(bg_map_normalized) == 1
vertexcolors_manually_normalized = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map_normalized)
assert len(vertexcolors_manually_normalized) == len(mesh.coordinates)
assert vertexcolors_manually_normalized == vertexcolors_auto_normalized
bg_map_scaled = bg_map_normalized / 2 + 0.25
assert np.min(bg_map_scaled) == 0.25 and np.max(bg_map_scaled) == 0.75
vertexcolors_manually_rescaled = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=bg_map_scaled)
assert len(vertexcolors_manually_rescaled) == len(mesh.coordinates)
assert vertexcolors_manually_rescaled != vertexcolors_auto_normalized
```

## Next Steps


---

*Source: test_matplotlib_backend.py:195 | Complexity: Advanced | Last updated: 2026-05-18*