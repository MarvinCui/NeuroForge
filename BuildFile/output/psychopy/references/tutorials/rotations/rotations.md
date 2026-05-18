# How To: Rotations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test rotations with quaternions and matrices. Checks if quaternions and
matrices constructed with the same axes and angles give the same rotations
to sets of random points.

Tests `quatFromAxisAngle`, `rotationMatrix`, `applyMatrix` and `applyQuat`.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test rotations with quaternions and matrices. Checks if quaternions and\n    matrices constructed with the same axes and angles give the same rotations\n    to sets of random points.\n\n    Tests `quatFromAxisAngle`, `rotationMatrix`, `applyMatrix` and `applyQuat`.\n\n    '

```python
'Test rotations with quaternions and matrices. Checks if quaternions and\n    matrices constructed with the same axes and angles give the same rotations\n    to sets of random points.\n\n    Tests `quatFromAxisAngle`, `rotationMatrix`, `applyMatrix` and `applyQuat`.\n\n    '
```

**Verification:**
```python
assert np.allclose(q, np.asarray([0.0, 0.0, 0.0, 1.0]))
```

### Step 2: Assign axis = value

```python
axis = [0.0, 0.0, -1.0]
```

**Verification:**
```python
assert np.allclose(q, np.identity(4))
```

### Step 3: Assign angle = 0.0

```python
angle = 0.0
```

**Verification:**
```python
assert np.allclose(applyMatrix(rotMat, points), applyQuat(rotQuat, points))
```

### Step 4: Assign q = quatFromAxisAngle(...)

```python
q = quatFromAxisAngle(axis, angle, degrees=True)
```

**Verification:**
```python
assert np.allclose(q, np.asarray([0.0, 0.0, 0.0, 1.0]))
```

### Step 5: Assign q = rotationMatrix(...)

```python
q = rotationMatrix(angle, axis)
```

**Verification:**
```python
assert np.allclose(q, np.identity(4))
```

### Step 6: Call np.random.seed()

```python
np.random.seed(123456)
```

### Step 7: Assign N = 1000

```python
N = 1000
```

### Step 8: Assign axes = np.random.uniform(...)

```python
axes = np.random.uniform(-1.0, 1.0, (N, 3))
```

### Step 9: Assign axes = normalize(...)

```python
axes = normalize(axes, out=axes)
```

### Step 10: Assign angles = np.random.uniform(...)

```python
angles = np.random.uniform(-180.0, 180.0, (N,))
```

### Step 11: Assign points = np.random.uniform(...)

```python
points = np.random.uniform(-100.0, 100.0, (N, 3))
```

### Step 12: Assign axis = value

```python
axis = axes[i, :]
```

### Step 13: Assign angle = value

```python
angle = angles[i]
```

### Step 14: Assign rotMat = value

```python
rotMat = rotationMatrix(angle, axis)[:3, :3]
```

### Step 15: Assign rotQuat = quatFromAxisAngle(...)

```python
rotQuat = quatFromAxisAngle(axis, angle, degrees=True)
```

**Verification:**
```python
assert np.allclose(applyMatrix(rotMat, points), applyQuat(rotQuat, points))
```


## Complete Example

```python
# Workflow
'Test rotations with quaternions and matrices. Checks if quaternions and\n    matrices constructed with the same axes and angles give the same rotations\n    to sets of random points.\n\n    Tests `quatFromAxisAngle`, `rotationMatrix`, `applyMatrix` and `applyQuat`.\n\n    '
axis = [0.0, 0.0, -1.0]
angle = 0.0
q = quatFromAxisAngle(axis, angle, degrees=True)
assert np.allclose(q, np.asarray([0.0, 0.0, 0.0, 1.0]))
q = rotationMatrix(angle, axis)
assert np.allclose(q, np.identity(4))
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
axes = normalize(axes, out=axes)
angles = np.random.uniform(-180.0, 180.0, (N,))
points = np.random.uniform(-100.0, 100.0, (N, 3))
for i in range(N):
    axis = axes[i, :]
    angle = angles[i]
    rotMat = rotationMatrix(angle, axis)[:3, :3]
    rotQuat = quatFromAxisAngle(axis, angle, degrees=True)
    assert np.allclose(applyMatrix(rotMat, points), applyQuat(rotQuat, points))
```

## Next Steps


---

*Source: test_mathtools.py:12 | Complexity: Advanced | Last updated: 2026-05-18*