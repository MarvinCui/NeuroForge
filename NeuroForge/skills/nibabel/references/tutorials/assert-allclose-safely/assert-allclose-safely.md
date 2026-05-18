# How To: Assert Allclose Safely

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test assert allclose safely

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `warnings`
- `numpy`
- `pytest`
- `casting`
- `testing`


## Step-by-Step Guide

### Step 1: Call assert_allclose_safely()

```python
assert_allclose_safely([1, 1], [1, 1])
```

**Verification:**
```python
assert_allclose_safely([1, 1], [1, 1])
```

### Step 2: Call assert_allclose_safely()

```python
assert_allclose_safely(1, 1)
```

**Verification:**
```python
assert_allclose_safely(1, 1)
```

### Step 3: Call assert_allclose_safely()

```python
assert_allclose_safely(1, [1, 1])
```

**Verification:**
```python
assert_allclose_safely(1, [1, 1])
```

### Step 4: Call assert_allclose_safely()

```python
assert_allclose_safely([1, 1], 1 + 1e-06)
```

**Verification:**
```python
assert_allclose_safely([1, 1], 1 + 1e-06)
```

### Step 5: Assign a = np.ones(...)

```python
a = np.ones((2, 3))
```

**Verification:**
```python
assert_allclose_safely([1, 1], 1 + 0.0001)
```

### Step 6: Assign b = np.ones(...)

```python
b = np.ones((3, 2, 3))
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 7: Assign eps = value

```python
eps = np.finfo(np.float64).eps
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 8: Assign unknown = value

```python
a[0, 0] = 1 + eps
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 9: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```

**Verification:**
```python
assert_allclose_safely(a, b, match_nans=False)
```

### Step 10: Assign unknown = value

```python
a[0, 0] = 1 + 1.1e-05
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 11: Assign unknown = value

```python
a[0, 0] = np.nan
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 12: Assign unknown = value

```python
b[:, 0, 0] = np.nan
```

**Verification:**
```python
assert_allclose_safely(a, b)
```

### Step 13: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```

**Verification:**
```python
assert_allclose_safely([], [])
```

### Step 14: Assign unknown = 1

```python
b[0, 0, 0] = 1
```

### Step 15: Call assert_allclose_safely()

```python
assert_allclose_safely([], [])
```

### Step 16: Call assert_allclose_safely()

```python
assert_allclose_safely([1, 1], 1 + 0.0001)
```

### Step 17: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```

### Step 18: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b, match_nans=False)
```

### Step 19: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```

### Step 20: Assign a = np.array(...)

```python
a = np.array([-np.inf, 1, np.inf], dtype=dtt)
```

### Step 21: Assign b = np.array(...)

```python
b = np.array([-np.inf, 1, np.inf], dtype=dtt)
```

### Step 22: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```

### Step 23: Assign unknown = 0

```python
b[1] = 0
```

### Step 24: Call assert_allclose_safely()

```python
assert_allclose_safely(a, b)
```


## Complete Example

```python
# Workflow
assert_allclose_safely([1, 1], [1, 1])
assert_allclose_safely(1, 1)
assert_allclose_safely(1, [1, 1])
assert_allclose_safely([1, 1], 1 + 1e-06)
with pytest.raises(AssertionError):
    assert_allclose_safely([1, 1], 1 + 0.0001)
a = np.ones((2, 3))
b = np.ones((3, 2, 3))
eps = np.finfo(np.float64).eps
a[0, 0] = 1 + eps
assert_allclose_safely(a, b)
a[0, 0] = 1 + 1.1e-05
with pytest.raises(AssertionError):
    assert_allclose_safely(a, b)
a[0, 0] = np.nan
b[:, 0, 0] = np.nan
assert_allclose_safely(a, b)
with pytest.raises(AssertionError):
    assert_allclose_safely(a, b, match_nans=False)
b[0, 0, 0] = 1
with pytest.raises(AssertionError):
    assert_allclose_safely(a, b)
for dtt in sctypes['float']:
    a = np.array([-np.inf, 1, np.inf], dtype=dtt)
    b = np.array([-np.inf, 1, np.inf], dtype=dtt)
    assert_allclose_safely(a, b)
    b[1] = 0
    with pytest.raises(AssertionError):
        assert_allclose_safely(a, b)
assert_allclose_safely([], [])
```

## Next Steps


---

*Source: test_testing.py:23 | Complexity: Advanced | Last updated: 2026-05-18*