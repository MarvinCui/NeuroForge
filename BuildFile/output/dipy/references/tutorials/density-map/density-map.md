# How To: Density Map

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test density map

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`


## Step-by-Step Guide

### Step 1: Assign streamlines = value

```python
streamlines = [np.array([np.arange(10)] * 3).T]
```

### Step 2: Assign shape = value

```python
shape = (10, 10, 10)
```

### Step 3: Assign x = np.arange(...)

```python
x = np.arange(10)
```

### Step 4: Assign expected = np.zeros(...)

```python
expected = np.zeros(shape)
```

### Step 5: Assign unknown = 1.0

```python
expected[x, x, x] = 1.0
```

### Step 6: Assign dm = density_map(...)

```python
dm = density_map(streamlines, np.eye(4), shape)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(dm, expected)
```

### Step 8: Call streamlines.append()

```python
streamlines.append(np.ones((5, 3)))
```

### Step 9: Assign shape = value

```python
shape = (5, 5, 5)
```

### Step 10: Assign x = np.arange(...)

```python
x = np.arange(5)
```

### Step 11: Assign expected = np.zeros(...)

```python
expected = np.zeros(shape)
```

### Step 12: Assign unknown = 1.0

```python
expected[x, x, x] = 1.0
```

### Step 13: Assign affine = value

```python
affine = np.eye(4) * 2
```

### Step 14: Assign unknown = 0.05

```python
affine[:3, 3] = 0.05
```

### Step 15: Assign dm = density_map(...)

```python
dm = density_map(streamlines, affine, shape)
```

### Step 16: Call npt.assert_array_equal()

```python
npt.assert_array_equal(dm, expected)
```

### Step 17: Assign dm = density_map(...)

```python
dm = density_map(iter(streamlines), affine, shape)
```

### Step 18: Call npt.assert_array_equal()

```python
npt.assert_array_equal(dm, expected)
```

### Step 19: Assign affine = np.diag(...)

```python
affine = np.diag([2, 2, 2, 1.0])
```

### Step 20: Assign unknown = 1.0

```python
affine[:3, 3] = 1.0
```

### Step 21: Assign dm = density_map(...)

```python
dm = density_map(streamlines, affine, shape)
```

### Step 22: Call npt.assert_array_equal()

```python
npt.assert_array_equal(dm, expected)
```

### Step 23: Assign expected_old = expected

```python
expected_old = expected
```

### Step 24: Assign new_shape = value

```python
new_shape = [i + 2 for i in shape]
```

### Step 25: Assign expected = np.zeros(...)

```python
expected = np.zeros(new_shape)
```

### Step 26: Assign unknown = expected_old

```python
expected[2:, 2:, 2:] = expected_old
```

### Step 27: Assign dm = density_map(...)

```python
dm = density_map(streamlines, affine, new_shape)
```

### Step 28: Call npt.assert_array_equal()

```python
npt.assert_array_equal(dm, expected)
```


## Complete Example

```python
# Workflow
streamlines = [np.array([np.arange(10)] * 3).T]
shape = (10, 10, 10)
x = np.arange(10)
expected = np.zeros(shape)
expected[x, x, x] = 1.0
dm = density_map(streamlines, np.eye(4), shape)
npt.assert_array_equal(dm, expected)
streamlines.append(np.ones((5, 3)))
shape = (5, 5, 5)
x = np.arange(5)
expected = np.zeros(shape)
expected[x, x, x] = 1.0
expected[0, 0, 0] += 1
affine = np.eye(4) * 2
affine[:3, 3] = 0.05
dm = density_map(streamlines, affine, shape)
npt.assert_array_equal(dm, expected)
dm = density_map(iter(streamlines), affine, shape)
npt.assert_array_equal(dm, expected)
affine = np.diag([2, 2, 2, 1.0])
affine[:3, 3] = 1.0
dm = density_map(streamlines, affine, shape)
npt.assert_array_equal(dm, expected)
affine[:3, 3] -= 4.0
expected_old = expected
new_shape = [i + 2 for i in shape]
expected = np.zeros(new_shape)
expected[2:, 2:, 2:] = expected_old
dm = density_map(streamlines, affine, new_shape)
npt.assert_array_equal(dm, expected)
```

## Next Steps


---

*Source: test_utils.py:47 | Complexity: Advanced | Last updated: 2026-05-18*