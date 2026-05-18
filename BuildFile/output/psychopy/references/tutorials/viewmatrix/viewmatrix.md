# How To: Viewmatrix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test view matrix generation.

This create a view matrix using `lookAt` and `viewMatrix` and checks if
they look at the same point.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test view matrix generation.\n\n    This create a view matrix using `lookAt` and `viewMatrix` and checks if\n    they look at the same point.\n\n    '

```python
'Test view matrix generation.\n\n    This create a view matrix using `lookAt` and `viewMatrix` and checks if\n    they look at the same point.\n\n    '
```

**Verification:**
```python
assert np.isclose(posOut0, posOut1).all()
```

### Step 2: Assign N = 1000

```python
N = 1000
```

### Step 3: Call np.random.seed()

```python
np.random.seed(12345)
```

### Step 4: Assign targets = np.random.uniform(...)

```python
targets = np.random.uniform(-100.0, 100.0, (N, 3))
```

### Step 5: Assign origin = value

```python
origin = [0, 0, 0]
```

### Step 6: Assign orthoProj = orthoProjectionMatrix(...)

```python
orthoProj = orthoProjectionMatrix(-1, 1, -1, 1, 0.1, 100)
```

### Step 7: Assign target = unknown.tolist(...)

```python
target = targets[i].tolist()
```

### Step 8: Assign V0 = viewMatrix(...)

```python
V0 = viewMatrix(origin, alignTo([0, 0, -1], target))
```

### Step 9: Assign V1 = lookAt(...)

```python
V1 = lookAt(origin, target, [0, 1, 0])
```

### Step 10: Assign posOut0 = pointToNdc(...)

```python
posOut0 = pointToNdc(target, V0, orthoProj)
```

### Step 11: Assign posOut1 = pointToNdc(...)

```python
posOut1 = pointToNdc(target, V1, orthoProj)
```

**Verification:**
```python
assert np.isclose(posOut0, posOut1).all()
```


## Complete Example

```python
# Workflow
'Test view matrix generation.\n\n    This create a view matrix using `lookAt` and `viewMatrix` and checks if\n    they look at the same point.\n\n    '
N = 1000
np.random.seed(12345)
targets = np.random.uniform(-100.0, 100.0, (N, 3))
origin = [0, 0, 0]
orthoProj = orthoProjectionMatrix(-1, 1, -1, 1, 0.1, 100)
for i in range(N):
    target = targets[i].tolist()
    V0 = viewMatrix(origin, alignTo([0, 0, -1], target))
    V1 = lookAt(origin, target, [0, 1, 0])
    posOut0 = pointToNdc(target, V0, orthoProj)
    posOut1 = pointToNdc(target, V1, orthoProj)
    assert np.isclose(posOut0, posOut1).all()
```

## Next Steps


---

*Source: test_viewtools.py:40 | Complexity: Advanced | Last updated: 2026-05-18*