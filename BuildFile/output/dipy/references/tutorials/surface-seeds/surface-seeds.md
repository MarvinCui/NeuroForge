# How To: Surface Seeds

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test surface seeds

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.tracking.mesh`


## Step-by-Step Guide

### Step 1: Assign eps = 1e-12

```python
eps = 1e-12
```

### Step 2: Assign unknown = create_cube(...)

```python
cube_tri, cube_vts = create_cube()
```

### Step 3: Assign nb_tri = len(...)

```python
nb_tri = len(cube_tri)
```

### Step 4: Assign nb_seed = 1000

```python
nb_seed = 1000
```

### Step 5: Assign unknown = random_coordinates_from_surface(...)

```python
tri_idx, trilin_coord = random_coordinates_from_surface(nb_tri, nb_seed)
```

### Step 6: Call npt.assert_array_less()

```python
npt.assert_array_less(-1, tri_idx)
```

### Step 7: Call npt.assert_array_less()

```python
npt.assert_array_less(tri_idx, nb_tri)
```

### Step 8: Call npt.assert_array_less()

```python
npt.assert_array_less(-eps, trilin_coord)
```

### Step 9: Call npt.assert_array_less()

```python
npt.assert_array_less(trilin_coord, 1.0 + eps)
```

### Step 10: Assign seed_pts = seeds_from_surface_coordinates(...)

```python
seed_pts = seeds_from_surface_coordinates(cube_tri, cube_vts, tri_idx, trilin_coord)
```

### Step 11: Call npt.assert_array_less()

```python
npt.assert_array_less(-eps, seed_pts)
```

### Step 12: Call npt.assert_array_less()

```python
npt.assert_array_less(seed_pts, 1.0 + eps)
```

### Step 13: Assign tri_mask = np.zeros(...)

```python
tri_mask = np.zeros([len(cube_tri)])
```

### Step 14: Assign unknown = 1.0

```python
tri_mask[i] = 1.0
```

### Step 15: Assign tri_maskb = tri_mask.astype(...)

```python
tri_maskb = tri_mask.astype(bool)
```

### Step 16: Assign unknown = random_coordinates_from_surface(...)

```python
t_idx, _ = random_coordinates_from_surface(nb_tri, nb_seed, triangles_mask=tri_maskb)
```

### Step 17: Call npt.assert_array_equal()

```python
npt.assert_array_equal(t_idx, i)
```

### Step 18: Assign unknown = random_coordinates_from_surface(...)

```python
t_idx, _ = random_coordinates_from_surface(nb_tri, nb_seed, triangles_weight=tri_mask)
```

### Step 19: Call npt.assert_array_equal()

```python
npt.assert_array_equal(t_idx, i)
```


## Complete Example

```python
# Workflow
eps = 1e-12
cube_tri, cube_vts = create_cube()
nb_tri = len(cube_tri)
nb_seed = 1000
tri_idx, trilin_coord = random_coordinates_from_surface(nb_tri, nb_seed)
npt.assert_array_less(-1, tri_idx)
npt.assert_array_less(tri_idx, nb_tri)
npt.assert_array_less(-eps, trilin_coord)
npt.assert_array_less(trilin_coord, 1.0 + eps)
seed_pts = seeds_from_surface_coordinates(cube_tri, cube_vts, tri_idx, trilin_coord)
npt.assert_array_less(-eps, seed_pts)
npt.assert_array_less(seed_pts, 1.0 + eps)
for i in range(len(cube_tri)):
    tri_mask = np.zeros([len(cube_tri)])
    tri_mask[i] = 1.0
    tri_maskb = tri_mask.astype(bool)
    t_idx, _ = random_coordinates_from_surface(nb_tri, nb_seed, triangles_mask=tri_maskb)
    npt.assert_array_equal(t_idx, i)
    t_idx, _ = random_coordinates_from_surface(nb_tri, nb_seed, triangles_weight=tri_mask)
    npt.assert_array_equal(t_idx, i)
```

## Next Steps


---

*Source: test_mesh.py:53 | Complexity: Advanced | Last updated: 2026-05-18*