# How To: Plot Surf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface.surf_plotting.plot_surf function with
available engine backends.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tempfile`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: plt, engine, tmp_path, in_memory_mesh, bg_map
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface.surf_plotting.plot_surf function with\n    available engine backends.\n    '

```python
'Test nilearn.plotting.surface.surf_plotting.plot_surf function with\n    available engine backends.\n    '
```

### Step 2: Assign alpha = None

```python
alpha = None
```

### Step 3: Assign cbar_vmin = None

```python
cbar_vmin = None
```

### Step 4: Assign cbar_vmax = None

```python
cbar_vmax = None
```

### Step 5: Call plot_surf()

```python
plot_surf(in_memory_mesh, engine=engine)
```

### Step 6: Call plot_surf()

```python
plot_surf(in_memory_mesh, bg_map=bg_map, engine=engine)
```

### Step 7: Call plot_surf()

```python
plot_surf(in_memory_mesh, bg_map=bg_map, alpha=alpha, output_file=tmp_path / 'tmp.png', engine=engine)
```

### Step 8: Call plot_surf()

```python
plot_surf(in_memory_mesh, bg_map=bg_map, colorbar=True, engine=engine)
```

### Step 9: Call plot_surf()

```python
plot_surf(in_memory_mesh, bg_map=bg_map, colorbar=True, cbar_vmin=cbar_vmin, cbar_vmax=cbar_vmax, cbar_tick_format='%i', engine=engine)
```

### Step 10: Assign alpha = 0.5

```python
alpha = 0.5
```

### Step 11: Assign cbar_vmin = 0

```python
cbar_vmin = 0
```

### Step 12: Assign cbar_vmax = 150

```python
cbar_vmax = 150
```


## Complete Example

```python
# Setup
# Fixtures: plt, engine, tmp_path, in_memory_mesh, bg_map

# Workflow
'Test nilearn.plotting.surface.surf_plotting.plot_surf function with\n    available engine backends.\n    '
alpha = None
cbar_vmin = None
cbar_vmax = None
if engine == 'matplotlib':
    alpha = 0.5
    cbar_vmin = 0
    cbar_vmax = 150
plot_surf(in_memory_mesh, engine=engine)
plot_surf(in_memory_mesh, bg_map=bg_map, engine=engine)
plot_surf(in_memory_mesh, bg_map=bg_map, alpha=alpha, output_file=tmp_path / 'tmp.png', engine=engine)
plot_surf(in_memory_mesh, bg_map=bg_map, colorbar=True, engine=engine)
plot_surf(in_memory_mesh, bg_map=bg_map, colorbar=True, cbar_vmin=cbar_vmin, cbar_vmax=cbar_vmax, cbar_tick_format='%i', engine=engine)
```

## Next Steps


---

*Source: test_surf_plotting.py:123 | Complexity: Advanced | Last updated: 2026-05-18*