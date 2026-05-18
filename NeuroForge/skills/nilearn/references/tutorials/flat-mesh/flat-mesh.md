# How To: Flat Mesh

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test flat mesh

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: xy
```

## Step-by-Step Guide

### Step 1: Assign mesh = flat_mesh(...)

```python
mesh = flat_mesh(xy[0], xy[1])
```

**Verification:**
```python
assert np.allclose(n, [0.0, 0.0, 1.0])
```

### Step 2: Assign points = value

```python
points = mesh.coordinates
```

### Step 3: Assign triangles = value

```python
triangles = mesh.faces
```

### Step 4: Assign unknown = value

```python
a, b, c = points[triangles[0]]
```

### Step 5: Assign n = np.cross(...)

```python
n = np.cross(b - a, c - a)
```

**Verification:**
```python
assert np.allclose(n, [0.0, 0.0, 1.0])
```


## Complete Example

```python
# Setup
# Fixtures: xy

# Workflow
mesh = flat_mesh(xy[0], xy[1])
points = mesh.coordinates
triangles = mesh.faces
a, b, c = points[triangles[0]]
n = np.cross(b - a, c - a)
assert np.allclose(n, [0.0, 0.0, 1.0])
```

## Next Steps


---

*Source: test_surface.py:446 | Complexity: Intermediate | Last updated: 2026-05-18*