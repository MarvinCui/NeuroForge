# How To: Kron Solve Lower

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test kron solve lower

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

### Step 2: Assign Ls = value

```python
Ls = [np.tril(np.random.rand(3, 3)) for i in range(3)]
```

### Step 3: Assign tot_size = np.prod(...)

```python
tot_size = np.prod([L.shape[1] for L in Ls])
```

### Step 4: Assign x = np.random.rand.reshape(...)

```python
x = np.random.rand(tot_size).reshape((tot_size, 1))
```

### Step 5: Assign big = kronecker(...)

```python
big = kronecker(*Ls)
```

### Step 6: Assign slow_ans = pt.linalg.solve_triangular(...)

```python
slow_ans = pt.linalg.solve_triangular(big, x, lower=True)
```

### Step 7: Assign fast_ans = kron_solve_lower(...)

```python
fast_ans = kron_solve_lower(Ls, x)
```

### Step 8: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(slow_ans.eval(), fast_ans.eval())
```


## Complete Example

```python
# Workflow
np.random.seed(1)
Ls = [np.tril(np.random.rand(3, 3)) for i in range(3)]
tot_size = np.prod([L.shape[1] for L in Ls])
x = np.random.rand(tot_size).reshape((tot_size, 1))
big = kronecker(*Ls)
slow_ans = pt.linalg.solve_triangular(big, x, lower=True)
fast_ans = kron_solve_lower(Ls, x)
np.testing.assert_array_almost_equal(slow_ans.eval(), fast_ans.eval())
```

## Next Steps


---

*Source: test_math.py:105 | Complexity: Advanced | Last updated: 2026-05-18*