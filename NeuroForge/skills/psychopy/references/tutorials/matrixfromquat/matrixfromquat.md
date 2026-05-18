# How To: Matrixfromquat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if a matrix created using `matrixFromQuat` is equivalent to a
rotation matrix created by `rotationMatrix`.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test if a matrix created using `matrixFromQuat` is equivalent to a\n    rotation matrix created by `rotationMatrix`.\n\n    '

```python
'Test if a matrix created using `matrixFromQuat` is equivalent to a\n    rotation matrix created by `rotationMatrix`.\n\n    '
```

**Verification:**
```python
assert np.allclose(qr, rm)
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

### Step 6: Assign q = quatFromAxisAngle(...)

```python
q = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
```

### Step 7: Assign qr = quatToMatrix(...)

```python
qr = quatToMatrix(q)
```

### Step 8: Assign rm = rotationMatrix(...)

```python
rm = rotationMatrix(angles[i], axes[i, :])
```

**Verification:**
```python
assert np.allclose(qr, rm)
```


## Complete Example

```python
# Workflow
'Test if a matrix created using `matrixFromQuat` is equivalent to a\n    rotation matrix created by `rotationMatrix`.\n\n    '
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(0.0, 360.0, (N,))
for i in range(N):
    q = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
    qr = quatToMatrix(q)
    rm = rotationMatrix(angles[i], axes[i, :])
    assert np.allclose(qr, rm)
```

## Next Steps


---

*Source: test_mathtools.py:67 | Complexity: Advanced | Last updated: 2026-05-18*