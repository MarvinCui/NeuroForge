# How To: Vertices To Triangles

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test vertices to triangles

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.tracking.mesh`


## Step-by-Step Guide

### Step 1: Assign unknown = create_cube(...)

```python
cube_tri, cube_vts = create_cube()
```

### Step 2: Assign vts_w = np.ones(...)

```python
vts_w = np.ones([len(cube_vts)])
```

### Step 3: Assign tri_w = vertices_to_triangles_values(...)

```python
tri_w = vertices_to_triangles_values(cube_tri, vts_w)
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(tri_w, 1.0)
```

### Step 5: Assign vts_w = np.zeros(...)

```python
vts_w = np.zeros([len(cube_vts)])
```

### Step 6: Assign unknown = 3.0

```python
vts_w[i] = 3.0
```

### Step 7: Assign tri_w_func = vertices_to_triangles_values(...)

```python
tri_w_func = vertices_to_triangles_values(cube_tri, vts_w)
```

### Step 8: Assign tri_w_manual = np.zeros(...)

```python
tri_w_manual = np.zeros([len(cube_tri)])
```

### Step 9: Call npt.assert_array_equal()

```python
npt.assert_array_equal(tri_w_func, tri_w_manual)
```


## Complete Example

```python
# Workflow
cube_tri, cube_vts = create_cube()
vts_w = np.ones([len(cube_vts)])
tri_w = vertices_to_triangles_values(cube_tri, vts_w)
npt.assert_array_equal(tri_w, 1.0)
for i in range(len(cube_vts)):
    vts_w = np.zeros([len(cube_vts)])
    vts_w[i] = 3.0
    tri_w_func = vertices_to_triangles_values(cube_tri, vts_w)
    tri_w_manual = np.zeros([len(cube_tri)])
    for j in range(len(cube_tri)):
        if i in cube_tri[j]:
            tri_w_manual[j] += 1.0
    npt.assert_array_equal(tri_w_func, tri_w_manual)
```

## Next Steps


---

*Source: test_mesh.py:88 | Complexity: Advanced | Last updated: 2026-05-18*