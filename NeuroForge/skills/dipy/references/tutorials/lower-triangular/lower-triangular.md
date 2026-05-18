# How To: Lower Triangular

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lower triangular

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign tensor = np.arange.reshape(...)

```python
tensor = np.arange(9).reshape((3, 3))
```

### Step 2: Assign D = lower_triangular(...)

```python
D = lower_triangular(tensor)
```

### Step 3: Call npt.assert_array_equal()

```python
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8])
```

### Step 4: Assign D = lower_triangular(...)

```python
D = lower_triangular(tensor, b0=1)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8, 0])
```

### Step 6: Assign D = lower_triangular(...)

```python
D = lower_triangular(tensor, b0=0)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8, 9])
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, lower_triangular, np.zeros((2, 3)))
```

### Step 9: Call npt.assert_raises()

```python
npt.assert_raises(TypeError, lower_triangular, tensor, b0='not a number')
```

### Step 10: Assign shape = value

```python
shape = (4, 5, 6)
```

### Step 11: Assign many_tensors = np.empty(...)

```python
many_tensors = np.empty(shape + (3, 3))
```

### Step 12: Assign unknown = tensor

```python
many_tensors[:] = tensor
```

### Step 13: Assign result = np.empty(...)

```python
result = np.empty(shape + (6,))
```

### Step 14: Assign unknown = value

```python
result[:] = [0, 3, 4, 6, 7, 8]
```

### Step 15: Assign D = lower_triangular(...)

```python
D = lower_triangular(many_tensors)
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(D, result)
```

### Step 17: Assign D = lower_triangular(...)

```python
D = lower_triangular(many_tensors, b0=1)
```

### Step 18: Assign result = np.empty(...)

```python
result = np.empty(shape + (7,))
```

### Step 19: Assign unknown = value

```python
result[:] = [0, 3, 4, 6, 7, 8, 0]
```

### Step 20: Call npt.assert_array_equal()

```python
npt.assert_array_equal(D, result)
```


## Complete Example

```python
# Workflow
tensor = np.arange(9).reshape((3, 3))
D = lower_triangular(tensor)
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8])
D = lower_triangular(tensor, b0=1)
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8, 0])
D = lower_triangular(tensor, b0=0)
npt.assert_array_equal(D, [0, 3, 4, 6, 7, 8, 9])
npt.assert_raises(ValueError, lower_triangular, np.zeros((2, 3)))
npt.assert_raises(TypeError, lower_triangular, tensor, b0='not a number')
shape = (4, 5, 6)
many_tensors = np.empty(shape + (3, 3))
many_tensors[:] = tensor
result = np.empty(shape + (6,))
result[:] = [0, 3, 4, 6, 7, 8]
D = lower_triangular(many_tensors)
npt.assert_array_equal(D, result)
D = lower_triangular(many_tensors, b0=1)
result = np.empty(shape + (7,))
result[:] = [0, 3, 4, 6, 7, 8, 0]
npt.assert_array_equal(D, result)
```

## Next Steps


---

*Source: test_dti.py:626 | Complexity: Advanced | Last updated: 2026-05-18*