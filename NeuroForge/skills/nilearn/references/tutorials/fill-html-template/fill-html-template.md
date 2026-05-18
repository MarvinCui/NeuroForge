# How To: Fill Html Template

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fill html template

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
# Fixtures: tmp_path, mni152_template_res_2, engine
```

## Step-by-Step Guide

### Step 1: Assign fsaverage = fetch_surf_fsaverage(...)

```python
fsaverage = fetch_surf_fsaverage()
```

### Step 2: Assign surf_mesh = load_surf_mesh(...)

```python
surf_mesh = load_surf_mesh(fsaverage['pial_right'])
```

### Step 3: Assign surf_map = value

```python
surf_map = surf_mesh.coordinates[:, 0]
```

### Step 4: Assign bg_map = load_surf_data(...)

```python
bg_map = load_surf_data(fsaverage['sulc_right'])
```

### Step 5: Assign surf_mesh = load_surf_mesh(...)

```python
surf_mesh = load_surf_mesh(surf_mesh)
```

### Step 6: Assign backend = get_surface_backend(...)

```python
backend = get_surface_backend(engine)
```

### Step 7: Assign info = backend._one_mesh_info(...)

```python
info = backend._one_mesh_info(surf_map=surf_map, surf_mesh=surf_mesh, threshold='90%', black_bg=True, bg_map=bg_map)
```

### Step 8: Assign unknown = None

```python
info['title'] = None
```

### Step 9: Assign html = _fill_html_template(...)

```python
html = _fill_html_template(info, engine=engine)
```

### Step 10: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, engine=engine)
```

### Step 11: Assign info = _full_brain_info(...)

```python
info = _full_brain_info(mni152_template_res_2)
```

### Step 12: Assign unknown = None

```python
info['title'] = None
```

### Step 13: Assign html = _fill_html_template(...)

```python
html = _fill_html_template(info, engine=engine)
```

### Step 14: Call check_html_surface_plots()

```python
check_html_surface_plots(tmp_path, html, engine=engine)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, mni152_template_res_2, engine

# Workflow
fsaverage = fetch_surf_fsaverage()
surf_mesh = load_surf_mesh(fsaverage['pial_right'])
surf_map = surf_mesh.coordinates[:, 0]
bg_map = load_surf_data(fsaverage['sulc_right'])
surf_mesh = load_surf_mesh(surf_mesh)
backend = get_surface_backend(engine)
info = backend._one_mesh_info(surf_map=surf_map, surf_mesh=surf_mesh, threshold='90%', black_bg=True, bg_map=bg_map)
info['title'] = None
html = _fill_html_template(info, engine=engine)
check_html_surface_plots(tmp_path, html, engine=engine)
info = _full_brain_info(mni152_template_res_2)
info['title'] = None
html = _fill_html_template(info, engine=engine)
check_html_surface_plots(tmp_path, html, engine=engine)
```

## Next Steps


---

*Source: test_html_surface.py:75 | Complexity: Advanced | Last updated: 2026-05-18*