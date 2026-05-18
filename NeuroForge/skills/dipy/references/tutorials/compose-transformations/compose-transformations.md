# How To: Compose Transformations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compose transformations

## Prerequisites

**Required Modules:**
- `itertools`
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.sphere_stats`
- `dipy.testing.decorators`
- `dipy.testing.spherepoints`


## Step-by-Step Guide

### Step 1: Assign A = np.eye(...)

```python
A = np.eye(4)
```

**Verification:**
```python
assert_array_equal(CBA, np.eye(4))
```

### Step 2: Assign unknown = 10

```python
A[0, -1] = 10
```

**Verification:**
```python
assert_raises(ValueError, compose_transformations, A)
```

### Step 3: Assign B = np.eye(...)

```python
B = np.eye(4)
```

### Step 4: Assign unknown = value

```python
B[0, -1] = -20
```

### Step 5: Assign C = np.eye(...)

```python
C = np.eye(4)
```

### Step 6: Assign unknown = 10

```python
C[0, -1] = 10
```

### Step 7: Assign CBA = compose_transformations(...)

```python
CBA = compose_transformations(A, B, C)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(CBA, np.eye(4))
```

### Step 9: Call assert_raises()

```python
assert_raises(ValueError, compose_transformations, A)
```


## Complete Example

```python
# Workflow
A = np.eye(4)
A[0, -1] = 10
B = np.eye(4)
B[0, -1] = -20
C = np.eye(4)
C[0, -1] = 10
CBA = compose_transformations(A, B, C)
assert_array_equal(CBA, np.eye(4))
assert_raises(ValueError, compose_transformations, A)
```

## Next Steps


---

*Source: test_geometry.py:251 | Complexity: Advanced | Last updated: 2026-05-18*