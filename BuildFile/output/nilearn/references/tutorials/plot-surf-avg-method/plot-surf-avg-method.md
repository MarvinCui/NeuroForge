# How To: Plot Surf Avg Method

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting.surface.surf_plotting.plot_surf for valid
values of avg_method.

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

### Step 1: 'Test nilearn.plotting.surface.surf_plotting.plot_surf for valid\n    values of avg_method.\n    '

```python
'Test nilearn.plotting.surface.surf_plotting.plot_surf for valid\n    values of avg_method.\n    '
```

**Verification:**
```python
assert_array_equal(cmap(agg_faces), display._axstack.as_list()[0].collections[0]._facecolors)
```

### Step 2: Assign faces = value

```python
faces = in_memory_mesh.faces
```

### Step 3: Assign ENGINE = 'matplotlib'

```python
ENGINE = 'matplotlib'
```

### Step 4: Call plot_surf()

```python
plot_surf(in_memory_mesh, surf_map=bg_map, avg_method=custom_avg_function, engine=ENGINE)
```

### Step 5: Assign display = plot_surf(...)

```python
display = plot_surf(in_memory_mesh, surf_map=bg_map, avg_method=method, engine=ENGINE)
```

### Step 6: Assign vmin = np.min(...)

```python
vmin = np.min(agg_faces)
```

### Step 7: Assign vmax = np.max(...)

```python
vmax = np.max(agg_faces)
```

### Step 8: Assign cmap = matplotlib_pyplot.get_cmap(...)

```python
cmap = matplotlib_pyplot.get_cmap(matplotlib_pyplot.rcParamsDefault['image.cmap'])
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(cmap(agg_faces), display._axstack.as_list()[0].collections[0]._facecolors)
```

### Step 10: Assign agg_faces = np.mean(...)

```python
agg_faces = np.mean(bg_map[faces], axis=1)
```

### Step 11: Assign agg_faces = np.median(...)

```python
agg_faces = np.median(bg_map[faces], axis=1)
```

### Step 12: Assign agg_faces = np.min(...)

```python
agg_faces = np.min(bg_map[faces], axis=1)
```

### Step 13: Assign agg_faces = np.max(...)

```python
agg_faces = np.max(bg_map[faces], axis=1)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, in_memory_mesh, bg_map

# Workflow
'Test nilearn.plotting.surface.surf_plotting.plot_surf for valid\n    values of avg_method.\n    '
faces = in_memory_mesh.faces
ENGINE = 'matplotlib'
for method in ['mean', 'median', 'min', 'max']:
    display = plot_surf(in_memory_mesh, surf_map=bg_map, avg_method=method, engine=ENGINE)
    if method == 'mean':
        agg_faces = np.mean(bg_map[faces], axis=1)
    elif method == 'median':
        agg_faces = np.median(bg_map[faces], axis=1)
    elif method == 'min':
        agg_faces = np.min(bg_map[faces], axis=1)
    elif method == 'max':
        agg_faces = np.max(bg_map[faces], axis=1)
    vmin = np.min(agg_faces)
    vmax = np.max(agg_faces)
    agg_faces -= vmin
    agg_faces /= vmax - vmin
    cmap = matplotlib_pyplot.get_cmap(matplotlib_pyplot.rcParamsDefault['image.cmap'])
    assert_array_equal(cmap(agg_faces), display._axstack.as_list()[0].collections[0]._facecolors)

def custom_avg_function(vertices):
    return vertices[0] * vertices[1] * vertices[2]
plot_surf(in_memory_mesh, surf_map=bg_map, avg_method=custom_avg_function, engine=ENGINE)
```

## Next Steps


---

*Source: test_surf_plotting.py:310 | Complexity: Advanced | Last updated: 2026-05-18*