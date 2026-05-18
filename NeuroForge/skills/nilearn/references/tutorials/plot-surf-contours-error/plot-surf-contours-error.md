# How To: Plot Surf Contours Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface.surf_plotting.plot_surf_contours for
invalid parameters.

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
# Fixtures: matplotlib_pyplot, rng, in_memory_mesh, parcellation
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting.surface.surf_plotting.plot_surf_contours for\n    invalid parameters.\n    '

```python
'Test nilearn.plotting.surface.surf_plotting.plot_surf_contours for\n    invalid parameters.\n    '
```

### Step 2: Assign invalid_parcellation = rng.uniform(...)

```python
invalid_parcellation = rng.uniform(size=in_memory_mesh.n_vertices)
```

### Step 3: Assign unknown = matplotlib_pyplot.subplots(...)

```python
_, axes = matplotlib_pyplot.subplots(1, 1)
```

### Step 4: Assign msg = 'All elements of colors .* matplotlib .* RGBA'

```python
msg = 'All elements of colors .* matplotlib .* RGBA'
```

### Step 5: Assign msg = 'Levels, labels, and colors argument .* same length or None.'

```python
msg = 'Levels, labels, and colors argument .* same length or None.'
```

### Step 6: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, invalid_parcellation)
```

### Step 7: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, parcellation, axes=axes)
```

### Step 8: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], colors=[[1, 2], 3])
```

### Step 9: Call plot_surf_contours()

```python
plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], colors=['r'], labels=['1', '2'])
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, rng, in_memory_mesh, parcellation

# Workflow
'Test nilearn.plotting.surface.surf_plotting.plot_surf_contours for\n    invalid parameters.\n    '
invalid_parcellation = rng.uniform(size=in_memory_mesh.n_vertices)
with pytest.raises(ValueError, match='Vertices in parcellation do not form region.'):
    plot_surf_contours(in_memory_mesh, invalid_parcellation)
_, axes = matplotlib_pyplot.subplots(1, 1)
with pytest.raises(ValueError, match='Axes must be 3D.'):
    plot_surf_contours(in_memory_mesh, parcellation, axes=axes)
msg = 'All elements of colors .* matplotlib .* RGBA'
with pytest.raises(ValueError, match=msg):
    plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], colors=[[1, 2], 3])
msg = 'Levels, labels, and colors argument .* same length or None.'
with pytest.raises(ValueError, match=msg):
    plot_surf_contours(in_memory_mesh, parcellation, levels=[1, 2], colors=['r'], labels=['1', '2'])
```

## Next Steps


---

*Source: test_surf_plotting.py:567 | Complexity: Advanced | Last updated: 2026-05-18*