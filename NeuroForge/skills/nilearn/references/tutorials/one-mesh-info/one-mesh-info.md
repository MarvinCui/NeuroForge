# How To: One Mesh Info

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface._plotly_backend._one_mesh_info.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.datasets`
- `nilearn.plotting.js_plotting_utils`
- `nilearn.plotting.surface._plotly_backend`
- `nilearn.plotting.surface._utils`
- `nilearn.plotting.tests.test_engine_utils`
- `nilearn.surface.surface`


## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface._plotly_backend._one_mesh_info.'

```python
'Test nilearn.plotting.surface._plotly_backend._one_mesh_info.'
```

**Verification:**
```python
assert {'_x', '_y', '_z', '_i', '_j', '_k'}.issubset(info['inflated_both'].keys())
```

### Step 2: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

**Verification:**
```python
assert len(decode(info['inflated_both']['_x'], '<f4')) == len(surf_map)
```

### Step 3: Assign mesh = value

```python
mesh = fsaverage['pial_left']
```

**Verification:**
```python
assert len(info['vertexcolor_both']) == len(surf_map)
```

### Step 4: Assign surf_map = load_surf_data(...)

```python
surf_map = load_surf_data(fsaverage['sulc_left'])
```

**Verification:**
```python
assert (info['cmin'], info['cmax']) == (-cmax, cmax)
```

### Step 5: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(mesh)
```

**Verification:**
```python
assert isinstance(info['cmax'], float)
```

### Step 6: Assign backend = get_surface_backend(...)

```python
backend = get_surface_backend('plotly')
```

**Verification:**
```python
assert info['black_bg']
```

### Step 7: Assign info = backend._one_mesh_info(...)

```python
info = backend._one_mesh_info(surf_map, mesh, '90%', black_bg=True, bg_map=surf_map)
```

**Verification:**
```python
assert not info['full_brain_mesh']
```

### Step 8: Assign cmax = np.max(...)

```python
cmax = np.max(np.abs(surf_map))
```

**Verification:**
```python
assert (info['cmin'], info['cmax']) == (-cmax, cmax)
```

### Step 9: Call check_colors()

```python
check_colors(info['colorscale'])
```


## Complete Example

```python
# Workflow
'Test nilearn.plotting.surface._plotly_backend._one_mesh_info.'
fsaverage = fetch_surf_fsaverage()
mesh = fsaverage['pial_left']
surf_map = load_surf_data(fsaverage['sulc_left'])
mesh = load_surf_mesh(mesh)
backend = get_surface_backend('plotly')
info = backend._one_mesh_info(surf_map, mesh, '90%', black_bg=True, bg_map=surf_map)
assert {'_x', '_y', '_z', '_i', '_j', '_k'}.issubset(info['inflated_both'].keys())
assert len(decode(info['inflated_both']['_x'], '<f4')) == len(surf_map)
assert len(info['vertexcolor_both']) == len(surf_map)
cmax = np.max(np.abs(surf_map))
assert (info['cmin'], info['cmax']) == (-cmax, cmax)
assert isinstance(info['cmax'], float)
assert info['black_bg']
assert not info['full_brain_mesh']
check_colors(info['colorscale'])
```

## Next Steps


---

*Source: test_plotly_backend.py:260 | Complexity: Advanced | Last updated: 2026-05-18*