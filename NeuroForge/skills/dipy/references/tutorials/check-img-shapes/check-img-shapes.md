# How To: Check Img Shapes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check img shapes

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.viz.horizon.util`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign affine = np.array(...)

```python
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
```

### Step 2: Assign data = value

```python
data = 255 * rng.random((197, 233, 189))
```

### Step 3: Assign data1 = value

```python
data1 = 255 * rng.random((197, 233, 189))
```

### Step 4: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (True, False))
```

### Step 6: Assign data1 = value

```python
data1 = 255 * rng.random((200, 233, 189))
```

### Step 7: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (False, False))
```

### Step 9: Assign data = value

```python
data = 255 * rng.random((197, 233, 189, 10))
```

### Step 10: Assign data1 = value

```python
data1 = 255 * rng.random((197, 233, 189))
```

### Step 11: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (True, True))
```

### Step 13: Assign data = value

```python
data = 255 * rng.random((197, 233, 189, 15))
```

### Step 14: Assign data1 = value

```python
data1 = 255 * rng.random((197, 233, 189, 15))
```

### Step 15: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 16: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (True, True))
```

### Step 17: Assign data = value

```python
data = 255 * rng.random((198, 233, 189, 14))
```

### Step 18: Assign data1 = value

```python
data1 = 255 * rng.random((198, 233, 189, 15))
```

### Step 19: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (True, False))
```

### Step 21: Assign data = value

```python
data = 255 * rng.random((197, 233, 189, 15))
```

### Step 22: Assign data1 = value

```python
data1 = 255 * rng.random((198, 233, 189, 14))
```

### Step 23: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 24: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (False, False))
```

### Step 25: Assign data = value

```python
data = 255 * rng.random((197, 233, 189, 15))
```

### Step 26: Assign data1 = value

```python
data1 = 255 * rng.random((198, 233, 189, 15))
```

### Step 27: Assign images = value

```python
images = [(data, affine), (data1, affine)]
```

### Step 28: Call npt.assert_equal()

```python
npt.assert_equal(check_img_shapes(images), (False, False))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
data = 255 * rng.random((197, 233, 189))
data1 = 255 * rng.random((197, 233, 189))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (True, False))
data1 = 255 * rng.random((200, 233, 189))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (False, False))
data = 255 * rng.random((197, 233, 189, 10))
data1 = 255 * rng.random((197, 233, 189))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (True, True))
data = 255 * rng.random((197, 233, 189, 15))
data1 = 255 * rng.random((197, 233, 189, 15))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (True, True))
data = 255 * rng.random((198, 233, 189, 14))
data1 = 255 * rng.random((198, 233, 189, 15))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (True, False))
data = 255 * rng.random((197, 233, 189, 15))
data1 = 255 * rng.random((198, 233, 189, 14))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (False, False))
data = 255 * rng.random((197, 233, 189, 15))
data1 = 255 * rng.random((198, 233, 189, 15))
images = [(data, affine), (data1, affine)]
npt.assert_equal(check_img_shapes(images), (False, False))
```

## Next Steps


---

*Source: test_util.py:17 | Complexity: Advanced | Last updated: 2026-05-18*