# How To: Fillpos

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fillpos

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `numpy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign xyz = np.zeros(...)

```python
xyz = np.zeros((3,))
```

### Step 2: Assign unknown = nq.fillpositive(...)

```python
w, x, y, z = nq.fillpositive(xyz)
```

### Step 3: yield (assert_true, w == 1)

```python
yield (assert_true, w == 1)
```

### Step 4: Assign xyz = value

```python
xyz = [0] * 3
```

### Step 5: Assign unknown = nq.fillpositive(...)

```python
w, x, y, z = nq.fillpositive(xyz)
```

### Step 6: yield (assert_true, w == 1)

```python
yield (assert_true, w == 1)
```

### Step 7: yield (assert_raises, ValueError, nq.fillpositive, [0, 0])

```python
yield (assert_raises, ValueError, nq.fillpositive, [0, 0])
```

### Step 8: yield (assert_raises, ValueError, nq.fillpositive, [0] * 4)

```python
yield (assert_raises, ValueError, nq.fillpositive, [0] * 4)
```

### Step 9: yield (assert_raises, ValueError, nq.fillpositive, [1.0] * 3)

```python
yield (assert_raises, ValueError, nq.fillpositive, [1.0] * 3)
```

### Step 10: Assign wxyz = nq.fillpositive(...)

```python
wxyz = nq.fillpositive([1, 0, 0])
```

### Step 11: yield (assert_true, wxyz[0] == 0.0)

```python
yield (assert_true, wxyz[0] == 0.0)
```


## Complete Example

```python
# Workflow
xyz = np.zeros((3,))
w, x, y, z = nq.fillpositive(xyz)
yield (assert_true, w == 1)
xyz = [0] * 3
w, x, y, z = nq.fillpositive(xyz)
yield (assert_true, w == 1)
yield (assert_raises, ValueError, nq.fillpositive, [0, 0])
yield (assert_raises, ValueError, nq.fillpositive, [0] * 4)
yield (assert_raises, ValueError, nq.fillpositive, [1.0] * 3)
wxyz = nq.fillpositive([1, 0, 0])
yield (assert_true, wxyz[0] == 0.0)
```

## Next Steps


---

*Source: test_quaternions.py:61 | Complexity: Advanced | Last updated: 2026-05-18*