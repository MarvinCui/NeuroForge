# How To: Q2Bg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test q2bg

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `numpy.testing`
- `dwiparams`


## Step-by-Step Guide

### Step 1: Assign q_vec = value

```python
q_vec = [0, 1e-06, 0]
```

**Verification:**
```python
assert_array_almost_equal(b, 0.0001)
```

### Step 2: Call np_assert_equal()

```python
np_assert_equal(q2bg(q_vec), (0, 0))
```

**Verification:**
```python
assert_array_almost_equal(g, [0, 1, 0])
```

### Step 3: Assign q_vec = value

```python
q_vec = [0, 0.0001, 0]
```

### Step 4: Assign unknown = q2bg(...)

```python
b, g = q2bg(q_vec)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(b, 0.0001)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(g, [0, 1, 0])
```

### Step 7: Call np_assert_equal()

```python
np_assert_equal(q2bg(q_vec, tol=0.0005), (0, 0))
```

### Step 8: Assign q_vec = np.zeros(...)

```python
q_vec = np.zeros((3,))
```

### Step 9: Assign unknown = 10.0

```python
q_vec[pos] = 10.0
```

### Step 10: Call np_assert_equal()

```python
np_assert_equal(q2bg(q_vec), (10, q_vec / 10.0))
```


## Complete Example

```python
# Workflow
for pos in range(3):
    q_vec = np.zeros((3,))
    q_vec[pos] = 10.0
    np_assert_equal(q2bg(q_vec), (10, q_vec / 10.0))
q_vec = [0, 1e-06, 0]
np_assert_equal(q2bg(q_vec), (0, 0))
q_vec = [0, 0.0001, 0]
b, g = q2bg(q_vec)
assert_array_almost_equal(b, 0.0001)
assert_array_almost_equal(g, [0, 1, 0])
np_assert_equal(q2bg(q_vec, tol=0.0005), (0, 0))
```

## Next Steps


---

*Source: test_dwiparams.py:42 | Complexity: Advanced | Last updated: 2026-05-18*