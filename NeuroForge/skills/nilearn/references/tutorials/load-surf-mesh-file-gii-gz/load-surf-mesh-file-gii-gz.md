# How To: Load Surf Mesh File Gii Gz

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test load surf mesh file gii gz

## Prerequisites

**Required Modules:**
- `warnings`
- `pathlib`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy.spatial`
- `scipy.stats`
- `sklearn.exceptions`
- `nilearn`
- `nilearn._utils`
- `nilearn._utils.helpers`
- `nilearn.image`
- `nilearn.surface.surface`


## Step-by-Step Guide

### Step 1: Assign fsaverage = value

```python
fsaverage = datasets.fetch_surf_fsaverage().pial_left
```

**Verification:**
```python
assert isinstance(coords, np.ndarray)
```

### Step 2: Assign mesh = load_surf_mesh(...)

```python
mesh = load_surf_mesh(fsaverage)
```

**Verification:**
```python
assert isinstance(faces, np.ndarray)
```

### Step 3: Assign coords = value

```python
coords = mesh.coordinates
```

### Step 4: Assign faces = value

```python
faces = mesh.faces
```

**Verification:**
```python
assert isinstance(coords, np.ndarray)
```


## Complete Example

```python
# Workflow
fsaverage = datasets.fetch_surf_fsaverage().pial_left
mesh = load_surf_mesh(fsaverage)
coords = mesh.coordinates
faces = mesh.faces
assert isinstance(coords, np.ndarray)
assert isinstance(faces, np.ndarray)
```

## Next Steps


---

*Source: test_surface.py:275 | Complexity: Intermediate | Last updated: 2026-05-18*