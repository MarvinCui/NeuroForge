# How To: B2Q

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test b2q

## Prerequisites

**Required Modules:**
- `numpy`
- `dwiparams`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign q = np.array(...)

```python
q = np.array([1, 2, 3])
```

**Verification:**
```python
assert_array_almost_equal(q * s, B2q(B))
```

### Step 2: Assign s = np.sqrt(...)

```python
s = np.sqrt(np.sum(q * q))
```

**Verification:**
```python
assert_array_almost_equal(q * s, B2q(B))
```

### Step 3: Assign B = np.outer(...)

```python
B = np.outer(q, q)
```

**Verification:**
```python
assert_array_almost_equal(-q * s, B2q(B))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(q * s, B2q(B))
```

**Verification:**
```python
assert_raises(ValueError, B2q, B)
```

### Step 5: Assign q = np.array(...)

```python
q = np.array([1, 2, 3])
```

### Step 6: Assign B = np.outer(...)

```python
B = np.outer(-q, -q)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(q * s, B2q(B))
```

### Step 8: Assign q = np.array(...)

```python
q = np.array([-1, 2, 3])
```

### Step 9: Assign B = np.outer(...)

```python
B = np.outer(q, q)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(-q * s, B2q(B))
```

### Step 11: Assign B = value

```python
B = np.eye(3) * -1
```

### Step 12: Call assert_raises()

```python
assert_raises(ValueError, B2q, B)
```

### Step 13: Assign q = B2q(...)

```python
q = B2q(B, tol=1)
```


## Complete Example

```python
# Workflow
q = np.array([1, 2, 3])
s = np.sqrt(np.sum(q * q))
B = np.outer(q, q)
assert_array_almost_equal(q * s, B2q(B))
q = np.array([1, 2, 3])
B = np.outer(-q, -q)
assert_array_almost_equal(q * s, B2q(B))
q = np.array([-1, 2, 3])
B = np.outer(q, q)
assert_array_almost_equal(-q * s, B2q(B))
B = np.eye(3) * -1
assert_raises(ValueError, B2q, B)
q = B2q(B, tol=1)
```

## Next Steps


---

*Source: test_dwiparams.py:15 | Complexity: Advanced | Last updated: 2026-05-18*