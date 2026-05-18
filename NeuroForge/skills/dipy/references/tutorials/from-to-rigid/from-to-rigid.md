# How To: From To Rigid

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test from to rigid

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.bundlemin`
- `dipy.align.streamlinear`
- `dipy.core.geometry`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign t = np.array(...)

```python
t = np.array([10, 2, 3, 0.1, 20.0, 30.0])
```

**Verification:**
```python
assert_array_almost_equal(t, vec)
```

### Step 2: Assign mat = compose_matrix44(...)

```python
mat = compose_matrix44(t)
```

**Verification:**
```python
assert_array_almost_equal(-t, vec)
```

### Step 3: Assign vec = decompose_matrix44(...)

```python
vec = decompose_matrix44(mat, size=6)
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(t, vec)
```

### Step 5: Assign t = np.array(...)

```python
t = np.array([0, 0, 0, 180, 0.0, 0.0])
```

### Step 6: Assign mat = np.eye(...)

```python
mat = np.eye(4)
```

### Step 7: Assign unknown = value

```python
mat[0, 0] = -1
```

### Step 8: Assign vec = decompose_matrix44(...)

```python
vec = decompose_matrix44(mat, size=6)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(-t, vec)
```


## Complete Example

```python
# Workflow
t = np.array([10, 2, 3, 0.1, 20.0, 30.0])
mat = compose_matrix44(t)
vec = decompose_matrix44(mat, size=6)
assert_array_almost_equal(t, vec)
t = np.array([0, 0, 0, 180, 0.0, 0.0])
mat = np.eye(4)
mat[0, 0] = -1
vec = decompose_matrix44(mat, size=6)
assert_array_almost_equal(-t, vec)
```

## Next Steps


---

*Source: test_streamlinear.py:301 | Complexity: Advanced | Last updated: 2026-05-18*