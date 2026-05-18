# How To: Multquat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test quaternion multiplication.

Create two quaternions, multiply them, and check if the resulting
orientation is as expected.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test quaternion multiplication.\n\n    Create two quaternions, multiply them, and check if the resulting\n    orientation is as expected.\n    '

```python
'Test quaternion multiplication.\n\n    Create two quaternions, multiply them, and check if the resulting\n    orientation is as expected.\n    '
```

**Verification:**
```python
assert np.allclose(multQuat(q0, q1), quatTarget)
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
angles = np.random.uniform(0.0, 360.0, (N, 2))
```

### Step 6: Assign totalAngle = value

```python
totalAngle = angles[i, 0] + angles[i, 1]
```

### Step 7: Assign q0 = quatFromAxisAngle(...)

```python
q0 = quatFromAxisAngle(axes[i, :], angles[i, 0], degrees=True)
```

### Step 8: Assign q1 = quatFromAxisAngle(...)

```python
q1 = quatFromAxisAngle(axes[i, :], angles[i, 1], degrees=True)
```

### Step 9: Assign quatTarget = quatFromAxisAngle(...)

```python
quatTarget = quatFromAxisAngle(axes[i, :], totalAngle, degrees=True)
```

**Verification:**
```python
assert np.allclose(multQuat(q0, q1), quatTarget)
```


## Complete Example

```python
# Workflow
'Test quaternion multiplication.\n\n    Create two quaternions, multiply them, and check if the resulting\n    orientation is as expected.\n    '
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(0.0, 360.0, (N, 2))
for i in range(N):
    totalAngle = angles[i, 0] + angles[i, 1]
    q0 = quatFromAxisAngle(axes[i, :], angles[i, 0], degrees=True)
    q1 = quatFromAxisAngle(axes[i, :], angles[i, 1], degrees=True)
    quatTarget = quatFromAxisAngle(axes[i, :], totalAngle, degrees=True)
    assert np.allclose(multQuat(q0, q1), quatTarget)
```

## Next Steps


---

*Source: test_mathtools.py:46 | Complexity: Advanced | Last updated: 2026-05-18*