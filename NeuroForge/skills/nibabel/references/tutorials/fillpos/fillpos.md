# How To: Fillpos

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fillpos

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign xyz = np.zeros(...)

```python
xyz = np.zeros((3,))
```

**Verification:**
```python
assert w == 1
```

### Step 2: Assign unknown = nq.fillpositive(...)

```python
w, x, y, z = nq.fillpositive(xyz)
```

**Verification:**
```python
assert w == 1
```

### Step 3: Assign xyz = value

```python
xyz = [0] * 3
```

**Verification:**
```python
assert wxyz[0] == 0.0
```

### Step 4: Assign unknown = nq.fillpositive(...)

```python
w, x, y, z = nq.fillpositive(xyz)
```

**Verification:**
```python
assert w == 1
```

### Step 5: Assign wxyz = nq.fillpositive(...)

```python
wxyz = nq.fillpositive([1, 0, 0])
```

**Verification:**
```python
assert wxyz[0] == 0.0
```

### Step 6: Call nq.fillpositive()

```python
nq.fillpositive([0, 0])
```

### Step 7: Call nq.fillpositive()

```python
nq.fillpositive([0] * 4)
```

### Step 8: Call nq.fillpositive()

```python
nq.fillpositive([1.0] * 3)
```


## Complete Example

```python
# Workflow
xyz = np.zeros((3,))
w, x, y, z = nq.fillpositive(xyz)
assert w == 1
xyz = [0] * 3
w, x, y, z = nq.fillpositive(xyz)
assert w == 1
with pytest.raises(ValueError):
    nq.fillpositive([0, 0])
with pytest.raises(ValueError):
    nq.fillpositive([0] * 4)
with pytest.raises(ValueError):
    nq.fillpositive([1.0] * 3)
wxyz = nq.fillpositive([1, 0, 0])
assert wxyz[0] == 0.0
```

## Next Steps


---

*Source: test_quaternions.py:55 | Complexity: Advanced | Last updated: 2026-05-18*