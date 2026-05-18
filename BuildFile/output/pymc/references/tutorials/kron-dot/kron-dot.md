# How To: Kron Dot

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test kron dot

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc.math`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 2: Assign Ks = value

```python
Ks = [np.random.rand(3, 3) for i in range(3)]
```

### Step 3: Assign tot_size = np.prod(...)

```python
tot_size = np.prod([k.shape[1] for k in Ks])
```

### Step 4: Assign x = np.random.rand.reshape(...)

```python
x = np.random.rand(tot_size).reshape((tot_size, 1))
```

### Step 5: Assign big = kronecker(...)

```python
big = kronecker(*Ks)
```

### Step 6: Assign slow_ans = pt.dot(...)

```python
slow_ans = pt.dot(big, x)
```

### Step 7: Assign fast_ans = kron_dot(...)

```python
fast_ans = kron_dot(Ks, x)
```

### Step 8: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(slow_ans.eval(), fast_ans.eval())
```


## Complete Example

```python
# Workflow
np.random.seed(1)
Ks = [np.random.rand(3, 3) for i in range(3)]
tot_size = np.prod([k.shape[1] for k in Ks])
x = np.random.rand(tot_size).reshape((tot_size, 1))
big = kronecker(*Ks)
slow_ans = pt.dot(big, x)
fast_ans = kron_dot(Ks, x)
np.testing.assert_array_almost_equal(slow_ans.eval(), fast_ans.eval())
```

## Next Steps


---

*Source: test_math.py:90 | Complexity: Advanced | Last updated: 2026-05-18*