# How To: Trilinear Interp Cubic Voxels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test trilinear interp cubic voxels

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.align`
- `dipy.core.interpolation`
- `dipy.core.subdivide_octahedron`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign A = np.ones(...)

```python
A = np.ones((17, 17, 17))
```

### Step 2: Assign B = np.zeros(...)

```python
B = np.zeros(3)
```

### Step 3: Assign strides = np.array(...)

```python
strides = np.array(A.strides, np.intp)
```

### Step 4: Assign unknown = 2

```python
A[7, 7, 7] = 2
```

### Step 5: Assign points = np.array(...)

```python
points = np.array([[0, 0, 0], [7.0, 7.5, 7.0], [3.5, 3.5, 3.5]])
```

### Step 6: Call map_coordinates_trilinear_iso()

```python
map_coordinates_trilinear_iso(A, points, strides, 3, B)
```

### Step 7: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(B, np.array([1.0, 1.5, 1.0]))
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A.copy(order='F'), points, strides, 3, B)
```

### Step 9: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points.copy(order='F'), strides, 3, B)
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points, stepped_1d(strides), 3, B)
```

### Step 11: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points, strides, 3, stepped_1d(B))
```


## Complete Example

```python
# Workflow
def stepped_1d(arr_1d):
    return np.vstack((arr_1d, arr_1d)).ravel(order='F')[::2]
A = np.ones((17, 17, 17))
B = np.zeros(3)
strides = np.array(A.strides, np.intp)
A[7, 7, 7] = 2
points = np.array([[0, 0, 0], [7.0, 7.5, 7.0], [3.5, 3.5, 3.5]])
map_coordinates_trilinear_iso(A, points, strides, 3, B)
npt.assert_array_almost_equal(B, np.array([1.0, 1.5, 1.0]))
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A.copy(order='F'), points, strides, 3, B)
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points.copy(order='F'), strides, 3, B)
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points, stepped_1d(strides), 3, B)
npt.assert_raises(ValueError, map_coordinates_trilinear_iso, A, points, strides, 3, stepped_1d(B))
```

## Next Steps


---

*Source: test_interpolation.py:356 | Complexity: Advanced | Last updated: 2026-05-18*