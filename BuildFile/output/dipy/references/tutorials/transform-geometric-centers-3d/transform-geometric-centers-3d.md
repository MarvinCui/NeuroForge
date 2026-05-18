# How To: Transform Geometric Centers 3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transform geometric centers 3d

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imaffine`
- `dipy.align.tests.test_parzenhist`
- `dipy.align.transforms`
- `dipy.core`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign axis = np.array(...)

```python
axis = np.array([0.5, 2.0, 1.5])
```

**Verification:**
```python
assert_array_almost_equal(actual.affine, expected)
```

### Step 2: Assign t = 0.15

```python
t = 0.15
```

### Step 3: Assign m_shapes = value

```python
m_shapes = [(256, 256, 128), (255, 255, 127), (64, 127, 142)]
```

### Step 4: Assign s_shapes = value

```python
s_shapes = [(256, 256, 128), (255, 255, 127), (64, 127, 142)]
```

### Step 5: Assign moving = np.ndarray(...)

```python
moving = np.ndarray(shape=shape_moving)
```

### Step 6: Assign static = np.ndarray(...)

```python
static = np.ndarray(shape=shape_static)
```

### Step 7: Assign trans = np.array(...)

```python
trans = np.array([[1, 0, 0, -t * shape_static[0]], [0, 1, 0, -t * shape_static[1]], [0, 0, 1, -t * shape_static[2]], [0, 0, 0, 1]])
```

### Step 8: Assign trans_inv = npl.inv(...)

```python
trans_inv = npl.inv(trans)
```

### Step 9: Assign rot = np.zeros(...)

```python
rot = np.zeros(shape=(4, 4))
```

### Step 10: Assign unknown = geometry.rodrigues_axis_rotation(...)

```python
rot[:3, :3] = geometry.rodrigues_axis_rotation(axis, theta)
```

### Step 11: Assign unknown = 1.0

```python
rot[3, 3] = 1.0
```

### Step 12: Assign scale = np.array(...)

```python
scale = np.array([[1 * s, 0, 0, 0], [0, 1 * s, 0, 0], [0, 0, 1 * s, 0], [0, 0, 0, 1]])
```

### Step 13: Assign static_grid2world = trans_inv.dot(...)

```python
static_grid2world = trans_inv.dot(scale.dot(rot.dot(trans)))
```

### Step 14: Assign moving_grid2world = npl.inv(...)

```python
moving_grid2world = npl.inv(static_grid2world)
```

### Step 15: Assign c_static = value

```python
c_static = np.array(shape_static, dtype=np.float64) * 0.5
```

### Step 16: Assign c_static = tuple(...)

```python
c_static = tuple(c_static)
```

### Step 17: Assign c_static = value

```python
c_static = static_grid2world.dot(c_static + (1,))[:3]
```

### Step 18: Assign c_moving = value

```python
c_moving = np.array(shape_moving, dtype=np.float64) * 0.5
```

### Step 19: Assign c_moving = tuple(...)

```python
c_moving = tuple(c_moving)
```

### Step 20: Assign c_moving = value

```python
c_moving = moving_grid2world.dot(c_moving + (1,))[:3]
```

### Step 21: Assign expected = np.eye(...)

```python
expected = np.eye(4)
```

### Step 22: Assign unknown = value

```python
expected[:3, 3] = c_moving - c_static
```

### Step 23: Assign actual = imaffine.transform_geometric_centers(...)

```python
actual = imaffine.transform_geometric_centers(static, static_grid2world, moving, moving_grid2world)
```

### Step 24: Call assert_array_almost_equal()

```python
assert_array_almost_equal(actual.affine, expected)
```


## Complete Example

```python
# Workflow
axis = np.array([0.5, 2.0, 1.5])
t = 0.15
for theta in [-1 * np.pi / 6.0, 0.0, np.pi / 5.0]:
    for s in [0.83, 1.3, 2.07]:
        m_shapes = [(256, 256, 128), (255, 255, 127), (64, 127, 142)]
        for shape_moving in m_shapes:
            s_shapes = [(256, 256, 128), (255, 255, 127), (64, 127, 142)]
            for shape_static in s_shapes:
                moving = np.ndarray(shape=shape_moving)
                static = np.ndarray(shape=shape_static)
                trans = np.array([[1, 0, 0, -t * shape_static[0]], [0, 1, 0, -t * shape_static[1]], [0, 0, 1, -t * shape_static[2]], [0, 0, 0, 1]])
                trans_inv = npl.inv(trans)
                rot = np.zeros(shape=(4, 4))
                rot[:3, :3] = geometry.rodrigues_axis_rotation(axis, theta)
                rot[3, 3] = 1.0
                scale = np.array([[1 * s, 0, 0, 0], [0, 1 * s, 0, 0], [0, 0, 1 * s, 0], [0, 0, 0, 1]])
                static_grid2world = trans_inv.dot(scale.dot(rot.dot(trans)))
                moving_grid2world = npl.inv(static_grid2world)
                c_static = np.array(shape_static, dtype=np.float64) * 0.5
                c_static = tuple(c_static)
                c_static = static_grid2world.dot(c_static + (1,))[:3]
                c_moving = np.array(shape_moving, dtype=np.float64) * 0.5
                c_moving = tuple(c_moving)
                c_moving = moving_grid2world.dot(c_moving + (1,))[:3]
                expected = np.eye(4)
                expected[:3, 3] = c_moving - c_static
                actual = imaffine.transform_geometric_centers(static, static_grid2world, moving, moving_grid2world)
                assert_array_almost_equal(actual.affine, expected)
```

## Next Steps


---

*Source: test_imaffine.py:104 | Complexity: Advanced | Last updated: 2026-05-18*