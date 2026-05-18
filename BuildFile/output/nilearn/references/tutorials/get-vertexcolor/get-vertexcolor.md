# How To: Get Vertexcolor

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test get_vertexcolor.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.surface._matplotlib_backend`
- `nilearn.surface`


## Step-by-Step Guide

### Step 1: 'Test get_vertexcolor.'

```python
'Test get_vertexcolor.'
```

**Verification:**
```python
assert len(vertexcolors) == len(mesh.coordinates)
```

### Step 2: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

**Verification:**
```python
assert len(vertexcolors) == len(mesh.coordinates)
```

### Step 3: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(fsaverage['pial_left'])
```

### Step 4: Assign surf_map = np.arange(...)

```python
surf_map = np.arange(len(mesh.coordinates))
```

### Step 5: Assign colors = colorscale(...)

```python
colors = colorscale('jet', surf_map, 10)
```

### Step 6: Assign vertexcolors = _get_vertexcolor(...)

```python
vertexcolors = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=fsaverage['sulc_left'])
```

**Verification:**
```python
assert len(vertexcolors) == len(mesh.coordinates)
```

### Step 7: Assign vertexcolors = _get_vertexcolor(...)

```python
vertexcolors = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'])
```

**Verification:**
```python
assert len(vertexcolors) == len(mesh.coordinates)
```


## Complete Example

```python
# Workflow
'Test get_vertexcolor.'
fsaverage = fetch_surf_fsaverage()
mesh = load_surf_mesh(fsaverage['pial_left'])
surf_map = np.arange(len(mesh.coordinates))
colors = colorscale('jet', surf_map, 10)
vertexcolors = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'], bg_map=fsaverage['sulc_left'])
assert len(vertexcolors) == len(mesh.coordinates)
vertexcolors = _get_vertexcolor(surf_map, colors['cmap'], colors['norm'], absolute_threshold=colors['abs_threshold'])
assert len(vertexcolors) == len(mesh.coordinates)
```

## Next Steps


---

*Source: test_matplotlib_backend.py:168 | Complexity: Intermediate | Last updated: 2026-05-18*