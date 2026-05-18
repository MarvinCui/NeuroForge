# How To: Triangles Area

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test triangles area

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

### Step 2: Assign area = triangles_area(...)

```python
area = triangles_area(cube_tri, cube_vts)
```

### Step 3: Call npt.assert_array_equal()

```python
npt.assert_array_equal(area, 0.5)
```

### Step 4: Assign area = triangles_area(...)

```python
area = triangles_area(cube_tri, cube_vts)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(area, 2.0)
```


## Complete Example

```python
# Workflow
cube_tri, cube_vts = create_cube()
area = triangles_area(cube_tri, cube_vts)
npt.assert_array_equal(area, 0.5)
cube_vts *= 2.0
area = triangles_area(cube_tri, cube_vts)
npt.assert_array_equal(area, 2.0)
```

## Next Steps


---

*Source: test_mesh.py:44 | Complexity: Intermediate | Last updated: 2026-05-18*