# How To: View Surf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test view surf

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `numpy`
- `pytest`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.plotting.js_plotting_utils`
- `nilearn.plotting.surface._utils`
- `nilearn.plotting.surface.html_surface`
- `nilearn.plotting.tests.test_engine_utils`
- `nilearn.plotting.tests.test_js_plotting_utils`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: tmp_path, rng, engine
```

## Step-by-Step Guide

### Step 1: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

### Step 2: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(fsaverage['pial_right'])
```

### Step 3: Assign surf_map = value

```python
surf_map = mesh.coordinates[:, 0]
```

### Step 4: Assign html = view_surf(...)

```python
html = view_surf(fsaverage['pial_right'], surf_map, fsaverage['sulc_right'], threshold='90%', engine=engine)
```

### Step 5: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, title='Surface plot', engine=engine)
```

### Step 6: Assign html = view_surf(...)

```python
html = view_surf(fsaverage['pial_right'], surf_map, fsaverage['sulc_right'], threshold=0.3, title='SOME_TITLE', engine=engine)
```

### Step 7: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, title='SOME_TITLE', engine=engine)
```

### Step 8: Assign html = view_surf(...)

```python
html = view_surf(fsaverage['pial_right'], engine=engine)
```

### Step 9: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, engine=engine)
```

### Step 10: Assign atlas = rng.integers(...)

```python
atlas = rng.integers(0, 10, size=len(mesh.coordinates))
```

### Step 11: Assign html = view_surf(...)

```python
html = view_surf(fsaverage['pial_left'], atlas, symmetric_cmap=False, engine=engine)
```

### Step 12: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, engine=engine)
```

### Step 13: Assign html = view_surf(...)

```python
html = view_surf(fsaverage['pial_right'], fsaverage['sulc_right'], threshold=None, cmap='Greys', engine=engine)
```

### Step 14: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, engine=engine)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, rng, engine

# Workflow
fsaverage = fetch_surf_fsaverage()
mesh = load_surf_mesh(fsaverage['pial_right'])
surf_map = mesh.coordinates[:, 0]
html = view_surf(fsaverage['pial_right'], surf_map, fsaverage['sulc_right'], threshold='90%', engine=engine)
check_html_surface_plots(tmp_path, html, title='Surface plot', engine=engine)
html = view_surf(fsaverage['pial_right'], surf_map, fsaverage['sulc_right'], threshold=0.3, title='SOME_TITLE', engine=engine)
check_html_surface_plots(tmp_path, html, title='SOME_TITLE', engine=engine)
html = view_surf(fsaverage['pial_right'], engine=engine)
check_html_surface_plots(tmp_path, html, engine=engine)
atlas = rng.integers(0, 10, size=len(mesh.coordinates))
html = view_surf(fsaverage['pial_left'], atlas, symmetric_cmap=False, engine=engine)
check_html_surface_plots(tmp_path, html, engine=engine)
html = view_surf(fsaverage['pial_right'], fsaverage['sulc_right'], threshold=None, cmap='Greys', engine=engine)
check_html_surface_plots(tmp_path, html, engine=engine)
```

## Next Steps


---

*Source: test_html_surface.py:106 | Complexity: Advanced | Last updated: 2026-05-18*