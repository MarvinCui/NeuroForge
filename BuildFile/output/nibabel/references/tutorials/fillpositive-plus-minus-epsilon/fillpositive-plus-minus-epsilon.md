# How To: Fillpositive Plus Minus Epsilon

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fillpositive plus minus epsilon

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`

**Setup Required:**
```python
# Fixtures: dtype
```

## Step-by-Step Guide

### Step 1: Assign nptype = value

```python
nptype = np.dtype(dtype).type
```

**Verification:**
```python
assert nq.fillpositive(plus)[0] == 0.0
```

### Step 2: Assign baseline = np.array(...)

```python
baseline = np.array([0, 0, 1], dtype=dtype)
```

**Verification:**
```python
assert nq.fillpositive(minus)[0] == 0.0
```

### Step 3: Assign plus = value

```python
plus = baseline * nptype(1 + np.finfo(dtype).eps)
```

**Verification:**
```python
assert nq.fillpositive(minus)[0] > 0.0
```

### Step 4: Assign minus = value

```python
minus = baseline * nptype(1 - np.finfo(dtype).eps)
```

**Verification:**
```python
assert nq.fillpositive(plus)[0] == 0.0
```

### Step 5: Assign plus = value

```python
plus = baseline * nptype(1 + 2 * np.finfo(dtype).eps)
```

### Step 6: Assign minus = value

```python
minus = baseline * nptype(1 - 2 * np.finfo(dtype).eps)
```

**Verification:**
```python
assert nq.fillpositive(minus)[0] > 0.0
```

### Step 7: Call nq.fillpositive()

```python
nq.fillpositive(plus)
```


## Complete Example

```python
# Setup
# Fixtures: dtype

# Workflow
nptype = np.dtype(dtype).type
baseline = np.array([0, 0, 1], dtype=dtype)
plus = baseline * nptype(1 + np.finfo(dtype).eps)
minus = baseline * nptype(1 - np.finfo(dtype).eps)
assert nq.fillpositive(plus)[0] == 0.0
assert nq.fillpositive(minus)[0] == 0.0
plus = baseline * nptype(1 + 2 * np.finfo(dtype).eps)
with pytest.raises(ValueError):
    nq.fillpositive(plus)
minus = baseline * nptype(1 - 2 * np.finfo(dtype).eps)
assert nq.fillpositive(minus)[0] > 0.0
```

## Next Steps


---

*Source: test_quaternions.py:78 | Complexity: Intermediate | Last updated: 2026-05-18*