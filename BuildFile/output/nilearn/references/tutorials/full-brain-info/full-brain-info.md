# How To: Full Brain Info

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full brain info

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
# Fixtures: mni152_template_res_2
```

## Step-by-Step Guide

### Step 1: Assign surfaces = fetch_surf_fsaverage(...)

```python
surfaces = fetch_surf_fsaverage()
```

**Verification:**
```python
assert {'pial_left', 'pial_right', 'inflated_left', 'inflated_right', 'vertexcolor_left', 'vertexcolor_right'}.issubset(info.keys())
```

### Step 2: Assign info = _full_brain_info(...)

```python
info = _full_brain_info(mni152_template_res_2, surfaces)
```

**Verification:**
```python
assert info['cmin'] == -info['cmax']
```

### Step 3: Call check_colors()

```python
check_colors(info['colorscale'])
```

**Verification:**
```python
assert info['full_brain_mesh']
```

### Step 4: Call json.dumps()

```python
json.dumps(info)
```

**Verification:**
```python
assert not info['black_bg']
```

### Step 5: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(surfaces[f'pial_{hemi}'])
```

**Verification:**
```python
assert isinstance(info['cmax'], float)
```


## Complete Example

```python
# Setup
# Fixtures: mni152_template_res_2

# Workflow
surfaces = fetch_surf_fsaverage()
info = _full_brain_info(mni152_template_res_2, surfaces)
check_colors(info['colorscale'])
assert {'pial_left', 'pial_right', 'inflated_left', 'inflated_right', 'vertexcolor_left', 'vertexcolor_right'}.issubset(info.keys())
assert info['cmin'] == -info['cmax']
assert info['full_brain_mesh']
assert not info['black_bg']
assert isinstance(info['cmax'], float)
json.dumps(info)
for hemi in ['left', 'right']:
    mesh = load_surf_mesh(surfaces[f'pial_{hemi}'])
    assert len(info[f'vertexcolor_{hemi}']) == len(mesh.coordinates)
    assert len(decode(info[f'inflated_{hemi}']['_z'], '<f4')) == len(mesh.coordinates)
    assert len(decode(info[f'pial_{hemi}']['_j'], '<i4')) == len(mesh.faces)
```

## Next Steps


---

*Source: test_html_surface.py:45 | Complexity: Intermediate | Last updated: 2026-05-18*