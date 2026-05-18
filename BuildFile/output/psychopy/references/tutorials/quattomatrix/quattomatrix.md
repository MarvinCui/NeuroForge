# How To: Quattomatrix

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test converting quaternions to matrices and vice-versa. The end result
should be the same transformed vectors.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test converting quaternions to matrices and vice-versa. The end result\n    should be the same transformed vectors.'

```python
'Test converting quaternions to matrices and vice-versa. The end result\n    should be the same transformed vectors.'
```

**Verification:**
```python
assert np.allclose(applyMatrix(m, vectors[i]), applyQuat(q, vectors[i]))
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

### Step 3: Assign N = 1000

```python
N = 1000
```

### Step 4: Assign axes = np.random.uniform(...)

```python
axes = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 5: Assign angles = np.random.uniform(...)

```python
angles = np.random.uniform(0.0, 360.0, (N,))
```

### Step 6: Assign vectors = normalize(...)

```python
vectors = normalize(np.random.uniform(-1.0, 1.0, (N, 3)))
```

### Step 7: Assign q = matrixToQuat(...)

```python
q = matrixToQuat(rotationMatrix(angles[i], normalize(axes[i, :])))
```

### Step 8: Assign m = quatToMatrix(...)

```python
m = quatToMatrix(quatFromAxisAngle(normalize(axes[i, :]), angles[i]))
```

**Verification:**
```python
assert np.allclose(applyMatrix(m, vectors[i]), applyQuat(q, vectors[i]))
```


## Complete Example

```python
# Workflow
'Test converting quaternions to matrices and vice-versa. The end result\n    should be the same transformed vectors.'
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(0.0, 360.0, (N,))
vectors = normalize(np.random.uniform(-1.0, 1.0, (N, 3)))
for i in range(N):
    q = matrixToQuat(rotationMatrix(angles[i], normalize(axes[i, :])))
    m = quatToMatrix(quatFromAxisAngle(normalize(axes[i, :]), angles[i]))
    assert np.allclose(applyMatrix(m, vectors[i]), applyQuat(q, vectors[i]))
```

## Next Steps


---

*Source: test_mathtools.py:132 | Complexity: Advanced | Last updated: 2026-05-18*