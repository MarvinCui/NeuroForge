# How To: Orthogonalize

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check the `orthogonalize()` function. This function nudges a vector to
be perpendicular with another (usually a normal). All orthogonalized vectors
should be perpendicular to the normal vector, having a dot product very
close to zero. This condition must occur in all cases for the test to
succeed.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Check the `orthogonalize()` function. This function nudges a vector to\n    be perpendicular with another (usually a normal). All orthogonalized vectors\n    should be perpendicular to the normal vector, having a dot product very\n    close to zero. This condition must occur in all cases for the test to\n    succeed.\n\n    '

```python
'Check the `orthogonalize()` function. This function nudges a vector to\n    be perpendicular with another (usually a normal). All orthogonalized vectors\n    should be perpendicular to the normal vector, having a dot product very\n    close to zero. This condition must occur in all cases for the test to\n    succeed.\n\n    '
```

**Verification:**
```python
assert np.allclose(result1, result2)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(567890)
```

**Verification:**
```python
assert np.allclose(dot(normals, result1), 0.0)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

### Step 4: Assign normals = np.zeros(...)

```python
normals = np.zeros((N, 3))
```

### Step 5: Assign unknown = 1.0

```python
normals[:, 1] = 1.0
```

### Step 6: Assign vec = np.random.uniform(...)

```python
vec = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 7: Call normalize()

```python
normalize(vec, out=vec)
```

### Step 8: Assign axes = np.random.uniform(...)

```python
axes = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 9: Assign angles = np.random.uniform(...)

```python
angles = np.random.uniform(-180.0, 180.0, (N,))
```

### Step 10: Call normalize()

```python
normalize(normals[:, :3], out=normals[:, :3])
```

### Step 11: Assign result1 = orthogonalize(...)

```python
result1 = orthogonalize(vec, normals)
```

### Step 12: Assign result2 = np.zeros_like(...)

```python
result2 = np.zeros_like(result1)
```

### Step 13: Call orthogonalize()

```python
orthogonalize(vec, normals, out=result2)
```

**Verification:**
```python
assert np.allclose(result1, result2)
```

### Step 14: Assign r = rotationMatrix(...)

```python
r = rotationMatrix(angles[i], axes[i, :])
```

### Step 15: Assign unknown = applyMatrix(...)

```python
normals[i, :] = applyMatrix(r, normals[i, :])
```


## Complete Example

```python
# Workflow
'Check the `orthogonalize()` function. This function nudges a vector to\n    be perpendicular with another (usually a normal). All orthogonalized vectors\n    should be perpendicular to the normal vector, having a dot product very\n    close to zero. This condition must occur in all cases for the test to\n    succeed.\n\n    '
np.random.seed(567890)
N = 1000
normals = np.zeros((N, 3))
normals[:, 1] = 1.0
vec = np.random.uniform(-1.0, 1.0, (N, 3))
normalize(vec, out=vec)
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(-180.0, 180.0, (N,))
for i in range(N):
    r = rotationMatrix(angles[i], axes[i, :])
    normals[i, :] = applyMatrix(r, normals[i, :])
normalize(normals[:, :3], out=normals[:, :3])
result1 = orthogonalize(vec, normals)
result2 = np.zeros_like(result1)
orthogonalize(vec, normals, out=result2)
assert np.allclose(result1, result2)
assert np.allclose(dot(normals, result1), 0.0)
```

## Next Steps


---

*Source: test_mathtools.py:515 | Complexity: Advanced | Last updated: 2026-05-18*