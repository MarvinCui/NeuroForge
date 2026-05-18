# How To: Plot Surf Roi Matplotlib Specific Nan Handling

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi
for NAN handling with matplotlib engine.

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
# Fixtures: matplotlib_pyplot, surface_image_parcellation
```

## Step-by-Step Guide

### Step 1: 'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for NAN handling with matplotlib engine.\n    '

```python
'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for NAN handling with matplotlib engine.\n    '
```

**Verification:**
```python
assert n_faces == (tmp._facecolors[:, 3] != 0).sum()
```

### Step 2: Assign unknown = value

```python
surface_image_parcellation.data.parts['left'][::2] = np.nan
```

### Step 3: Assign img = plot_surf_roi(...)

```python
img = plot_surf_roi(surface_image_parcellation.mesh, roi_map=surface_image_parcellation, engine='matplotlib', hemi='left')
```

### Step 4: Assign tmp = value

```python
tmp = img._axstack.as_list()[0].collections[0]
```

### Step 5: Assign n_faces = value

```python
n_faces = surface_image_parcellation.mesh.parts['left'].faces.shape[0]
```

**Verification:**
```python
assert n_faces == (tmp._facecolors[:, 3] != 0).sum()
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, surface_image_parcellation

# Workflow
'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for NAN handling with matplotlib engine.\n    '
surface_image_parcellation.data.parts['left'][::2] = np.nan
img = plot_surf_roi(surface_image_parcellation.mesh, roi_map=surface_image_parcellation, engine='matplotlib', hemi='left')
tmp = img._axstack.as_list()[0].collections[0]
n_faces = surface_image_parcellation.mesh.parts['left'].faces.shape[0]
assert n_faces == (tmp._facecolors[:, 3] != 0).sum()
```

## Next Steps


---

*Source: test_surf_plotting.py:985 | Complexity: Intermediate | Last updated: 2026-05-18*