# How To: Expand Packed Triangular

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test expand packed triangular

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

### Step 1: Assign N = 5

```python
N = 5
```

**Verification:**
```python
assert np.all(expand_lower.eval({packed: lower_packed}) == lower)
```

### Step 2: Assign packed = pt.vector(...)

```python
packed = pt.vector('packed')
```

**Verification:**
```python
assert np.all(expand_upper.eval({packed: upper_packed}) == upper)
```

### Step 3: Call np.random.seed()

```python
np.random.seed(42)
```

**Verification:**
```python
assert np.all(expand_diag_lower.eval({packed: lower_packed}) == floatX(np.diag(vals)))
```

### Step 4: Assign vals = np.random.randn(...)

```python
vals = np.random.randn(N, N)
```

**Verification:**
```python
assert np.all(expand_diag_upper.eval({packed: upper_packed}) == floatX(np.diag(vals)))
```

### Step 5: Assign lower = floatX(...)

```python
lower = floatX(np.tril(vals))
```

### Step 6: Assign lower_packed = floatX(...)

```python
lower_packed = floatX(vals[lower != 0])
```

### Step 7: Assign upper = floatX(...)

```python
upper = floatX(np.triu(vals))
```

### Step 8: Assign upper_packed = floatX(...)

```python
upper_packed = floatX(vals[upper != 0])
```

### Step 9: Assign expand_lower = expand_packed_triangular(...)

```python
expand_lower = expand_packed_triangular(N, packed, lower=True)
```

### Step 10: Assign expand_upper = expand_packed_triangular(...)

```python
expand_upper = expand_packed_triangular(N, packed, lower=False)
```

### Step 11: Assign expand_diag_lower = expand_packed_triangular(...)

```python
expand_diag_lower = expand_packed_triangular(N, packed, lower=True, diagonal_only=True)
```

### Step 12: Assign expand_diag_upper = expand_packed_triangular(...)

```python
expand_diag_upper = expand_packed_triangular(N, packed, lower=False, diagonal_only=True)
```

**Verification:**
```python
assert np.all(expand_lower.eval({packed: lower_packed}) == lower)
```

### Step 13: Assign x = pt.matrix(...)

```python
x = pt.matrix('x')
```

### Step 14: Call expand_packed_triangular()

```python
expand_packed_triangular(5, x)
```

### Step 15: Call expand_packed_triangular()

```python
expand_packed_triangular(packed.shape[0], packed)
```


## Complete Example

```python
# Workflow
with pytest.raises(ValueError):
    x = pt.matrix('x')
    expand_packed_triangular(5, x)
N = 5
packed = pt.vector('packed')
with pytest.raises(TypeError):
    expand_packed_triangular(packed.shape[0], packed)
np.random.seed(42)
vals = np.random.randn(N, N)
lower = floatX(np.tril(vals))
lower_packed = floatX(vals[lower != 0])
upper = floatX(np.triu(vals))
upper_packed = floatX(vals[upper != 0])
expand_lower = expand_packed_triangular(N, packed, lower=True)
expand_upper = expand_packed_triangular(N, packed, lower=False)
expand_diag_lower = expand_packed_triangular(N, packed, lower=True, diagonal_only=True)
expand_diag_upper = expand_packed_triangular(N, packed, lower=False, diagonal_only=True)
assert np.all(expand_lower.eval({packed: lower_packed}) == lower)
assert np.all(expand_upper.eval({packed: upper_packed}) == upper)
assert np.all(expand_diag_lower.eval({packed: lower_packed}) == floatX(np.diag(vals)))
assert np.all(expand_diag_upper.eval({packed: upper_packed}) == floatX(np.diag(vals)))
```

## Next Steps


---

*Source: test_math.py:184 | Complexity: Advanced | Last updated: 2026-05-18*