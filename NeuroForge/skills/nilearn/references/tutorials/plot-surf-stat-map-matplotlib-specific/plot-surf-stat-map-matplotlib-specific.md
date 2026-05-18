# How To: Plot Surf Stat Map Matplotlib Specific

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface.surf_plotting.plot_surf_stat_map for
matplotlib engine specific parameters.

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
# Fixtures: matplotlib_pyplot, in_memory_mesh, bg_map
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface.surf_plotting.plot_surf_stat_map for\n    matplotlib engine specific parameters.\n    '

```python
'Test nilearn.plotting.surface.surf_plotting.plot_surf_stat_map for\n    matplotlib engine specific parameters.\n    '
```

**Verification:**
```python
assert len(fig.axes) == 1
```

### Step 2: Assign axes = value

```python
axes = matplotlib_pyplot.subplots(ncols=2, subplot_kw={'projection': '3d'})[1]
```

**Verification:**
```python
assert len(fig.axes) == 2
```

### Step 3: Assign axes = value

```python
axes = matplotlib_pyplot.subplots(ncols=2, subplot_kw={'projection': '3d'})[1]
```

**Verification:**
```python
assert float(first) == -float(last)
```

### Step 4: Assign fig = plot_surf_stat_map(...)

```python
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, colorbar=False)
```

**Verification:**
```python
assert len(fig.axes) == 2
```

### Step 5: Assign fig = plot_surf_stat_map(...)

```python
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, symmetric_cbar=True)
```

**Verification:**
```python
assert float(first) != -float(last)
```

### Step 6: Call fig.canvas.draw()

```python
fig.canvas.draw()
```

**Verification:**
```python
assert in_memory_mesh.faces.shape[0] == (tmp._facecolors[:, 3] != 0).sum()
```

### Step 7: Assign yticklabels = unknown.get_yticklabels(...)

```python
yticklabels = fig.axes[1].get_yticklabels()
```

### Step 8: Assign unknown = value

```python
first, last = (yticklabels[0].get_text(), yticklabels[-1].get_text())
```

**Verification:**
```python
assert float(first) == -float(last)
```

### Step 9: Assign fig = plot_surf_stat_map(...)

```python
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, symmetric_cbar=False)
```

### Step 10: Call fig.canvas.draw()

```python
fig.canvas.draw()
```

**Verification:**
```python
assert len(fig.axes) == 2
```

### Step 11: Assign yticklabels = unknown.get_yticklabels(...)

```python
yticklabels = fig.axes[1].get_yticklabels()
```

### Step 12: Assign unknown = value

```python
first, last = (yticklabels[0].get_text(), yticklabels[-1].get_text())
```

**Verification:**
```python
assert float(first) != -float(last)
```

### Step 13: Assign unknown = value

```python
bg_map[2] = np.nan
```

### Step 14: Assign fig = plot_surf_stat_map(...)

```python
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map)
```

### Step 15: Assign tmp = value

```python
tmp = fig._axstack.as_list()[0].collections[0]
```

**Verification:**
```python
assert in_memory_mesh.faces.shape[0] == (tmp._facecolors[:, 3] != 0).sum()
```

### Step 16: Call plot_surf_stat_map()

```python
plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, axes=ax)
```

### Step 17: Call plot_surf_stat_map()

```python
plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, axes=ax)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, in_memory_mesh, bg_map

# Workflow
'Test nilearn.plotting.surface.surf_plotting.plot_surf_stat_map for\n    matplotlib engine specific parameters.\n    '
axes = matplotlib_pyplot.subplots(ncols=2, subplot_kw={'projection': '3d'})[1]
for ax in axes.flatten():
    plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, axes=ax)
axes = matplotlib_pyplot.subplots(ncols=2, subplot_kw={'projection': '3d'})[1]
for ax in axes.flatten():
    plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, axes=ax)
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, colorbar=False)
assert len(fig.axes) == 1
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, symmetric_cbar=True)
fig.canvas.draw()
assert len(fig.axes) == 2
yticklabels = fig.axes[1].get_yticklabels()
first, last = (yticklabels[0].get_text(), yticklabels[-1].get_text())
assert float(first) == -float(last)
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map, symmetric_cbar=False)
fig.canvas.draw()
assert len(fig.axes) == 2
yticklabels = fig.axes[1].get_yticklabels()
first, last = (yticklabels[0].get_text(), yticklabels[-1].get_text())
assert float(first) != -float(last)
bg_map[2] = np.nan
fig = plot_surf_stat_map(in_memory_mesh, stat_map=bg_map)
tmp = fig._axstack.as_list()[0].collections[0]
assert in_memory_mesh.faces.shape[0] == (tmp._facecolors[:, 3] != 0).sum()
```

## Next Steps


---

*Source: test_surf_plotting.py:788 | Complexity: Advanced | Last updated: 2026-05-18*