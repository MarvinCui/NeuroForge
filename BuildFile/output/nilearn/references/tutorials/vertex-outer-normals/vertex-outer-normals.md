# How To: Vertex Outer Normals

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vertex outer normals

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

### Step 1: Assign mesh = flat_mesh(...)

```python
mesh = flat_mesh(5, 7)
```

**Verification:**
```python
assert_array_almost_equal(computed_normals, true_normals)
```

### Step 2: Assign computed_normals = _vertex_outer_normals(...)

```python
computed_normals = _vertex_outer_normals(mesh)
```

### Step 3: Assign true_normals = np.zeros(...)

```python
true_normals = np.zeros((len(mesh.coordinates), 3))
```

### Step 4: Assign unknown = 1

```python
true_normals[:, 2] = 1
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(computed_normals, true_normals)
```


## Complete Example

```python
# Workflow
mesh = flat_mesh(5, 7)
computed_normals = _vertex_outer_normals(mesh)
true_normals = np.zeros((len(mesh.coordinates), 3))
true_normals[:, 2] = 1
assert_array_almost_equal(computed_normals, true_normals)
```

## Next Steps


---

*Source: test_surface.py:455 | Complexity: Intermediate | Last updated: 2026-05-18*