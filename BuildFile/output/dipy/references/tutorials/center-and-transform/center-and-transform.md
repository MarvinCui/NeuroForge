# How To: Center And Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test center and transform

## Prerequisites

**Required Modules:**
- `types`
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`
- `dipy.tracking.streamlinespeed`


## Step-by-Step Guide

### Step 1: Assign A = np.array(...)

```python
A = np.array([[1, 2, 3], [1, 2, 3.0]])
```

**Verification:**
```python
assert_array_equal(streamlines2[0], B)
```

### Step 2: Assign streamlines = value

```python
streamlines = [A for _ in range(10)]
```

**Verification:**
```python
assert_array_equal(center, A[0])
```

### Step 3: Assign unknown = center_streamlines(...)

```python
streamlines2, center = center_streamlines(streamlines)
```

**Verification:**
```python
assert_array_equal(streamlines3[0], B)
```

### Step 4: Assign B = np.zeros(...)

```python
B = np.zeros((2, 3))
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(streamlines2[0], B)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(center, A[0])
```

### Step 7: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 8: Assign unknown = 2

```python
affine[0, 0] = 2
```

### Step 9: Assign unknown = value

```python
affine[:3, -1] = -np.array([2, 1, 1]) * center
```

### Step 10: Assign streamlines3 = transform_streamlines(...)

```python
streamlines3 = transform_streamlines(streamlines, affine)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(streamlines3[0], B)
```


## Complete Example

```python
# Workflow
A = np.array([[1, 2, 3], [1, 2, 3.0]])
streamlines = [A for _ in range(10)]
streamlines2, center = center_streamlines(streamlines)
B = np.zeros((2, 3))
assert_array_equal(streamlines2[0], B)
assert_array_equal(center, A[0])
affine = np.eye(4)
affine[0, 0] = 2
affine[:3, -1] = -np.array([2, 1, 1]) * center
streamlines3 = transform_streamlines(streamlines, affine)
assert_array_equal(streamlines3[0], B)
```

## Next Steps


---

*Source: test_streamline.py:633 | Complexity: Advanced | Last updated: 2026-05-18*