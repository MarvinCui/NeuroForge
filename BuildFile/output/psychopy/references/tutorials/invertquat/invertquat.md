# How To: Invertquat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if quaternion inversion works. When multiplied, the result should be
an identity quaternion.

## Prerequisites

**Required Modules:**
- `psychopy.tools.mathtools`
- `psychopy.tools.viewtools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: 'Test if quaternion inversion works. When multiplied, the result should be\n    an identity quaternion.\n\n    '

```python
'Test if quaternion inversion works. When multiplied, the result should be\n    an identity quaternion.\n\n    '
```

**Verification:**
```python
assert np.allclose(multQuat(q, qinv), qidt)
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

### Step 6: Assign qidt = np.array(...)

```python
qidt = np.array([0.0, 0.0, 0.0, 1.0])
```

### Step 7: Assign q = quatFromAxisAngle(...)

```python
q = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
```

### Step 8: Assign qinv = invertQuat(...)

```python
qinv = invertQuat(q)
```

**Verification:**
```python
assert np.allclose(multQuat(q, qinv), qidt)
```


## Complete Example

```python
# Workflow
'Test if quaternion inversion works. When multiplied, the result should be\n    an identity quaternion.\n\n    '
np.random.seed(123456)
N = 1000
axes = np.random.uniform(-1.0, 1.0, (N, 3))
angles = np.random.uniform(0.0, 360.0, (N,))
qidt = np.array([0.0, 0.0, 0.0, 1.0])
for i in range(N):
    q = quatFromAxisAngle(axes[i, :], angles[i], degrees=True)
    qinv = invertQuat(q)
    assert np.allclose(multQuat(q, qinv), qidt)
```

## Next Steps


---

*Source: test_mathtools.py:89 | Complexity: Advanced | Last updated: 2026-05-18*