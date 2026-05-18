# How To: Basic Training

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test basic training

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign dim = 10000

```python
dim = 10000
```

**Verification:**
```python
assert out.shape[1] == 5, 'Wrong output_dim'
```

### Step 2: Assign freqs = value

```python
freqs = [2 * numx.pi * 100.0, 2 * numx.pi * 500.0]
```

**Verification:**
```python
assert_array_almost_equal(abs(correlation), numx.eye(2), decimal - 3)
```

### Step 3: Assign t = numx.linspace(...)

```python
t = numx.linspace(0, 1, num=dim)
```

**Verification:**
```python
assert_array_almost_equal(outq, out[:, nr], decimal)
```

### Step 4: Assign mat = value

```python
mat = numx.array([numx.sin(freqs[0] * t), numx.sin(freqs[1] * t)]).T
```

**Verification:**
```python
assert out.shape[1] == 2, 'Wrong output_dim'
```

### Step 5: Assign mat = value

```python
mat = (mat - mean(mat[:-1, :], axis=0)) / std(mat[:-1, :], axis=0)
```

**Verification:**
```python
assert_array_almost_equal(abs(correlation), numx.eye(1), decimal - 3)
```

### Step 6: Assign des_mat = mat.copy(...)

```python
des_mat = mat.copy()
```

### Step 7: Assign mat = value

```python
mat = mult(mat, uniform((2, 2))) + uniform(2)
```

### Step 8: Assign sfa = mdp.nodes.SFA2Node(...)

```python
sfa = mdp.nodes.SFA2Node()
```

### Step 9: Call sfa.train()

```python
sfa.train(mat)
```

### Step 10: Assign out = sfa.execute(...)

```python
out = sfa.execute(mat)
```

**Verification:**
```python
assert out.shape[1] == 5, 'Wrong output_dim'
```

### Step 11: Assign correlation = value

```python
correlation = mult(des_mat[:-1, :].T, numx.take(out[:-1, :], (0, 2), axis=1)) / (dim - 2)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(correlation), numx.eye(2), decimal - 3)
```

### Step 13: Assign sfa = mdp.nodes.SFANode(...)

```python
sfa = mdp.nodes.SFANode(output_dim=2)
```

### Step 14: Call sfa.train()

```python
sfa.train(mat)
```

### Step 15: Assign out = sfa.execute(...)

```python
out = sfa.execute(mat)
```

**Verification:**
```python
assert out.shape[1] == 2, 'Wrong output_dim'
```

### Step 16: Assign correlation = value

```python
correlation = mult(des_mat[:-1, :1].T, out[:-1, :1]) / (dim - 2)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(correlation), numx.eye(1), decimal - 3)
```

### Step 18: Assign qform = sfa.get_quadratic_form(...)

```python
qform = sfa.get_quadratic_form(nr)
```

### Step 19: Assign outq = qform.apply(...)

```python
outq = qform.apply(mat)
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(outq, out[:, nr], decimal)
```


## Complete Example

```python
# Workflow
dim = 10000
freqs = [2 * numx.pi * 100.0, 2 * numx.pi * 500.0]
t = numx.linspace(0, 1, num=dim)
mat = numx.array([numx.sin(freqs[0] * t), numx.sin(freqs[1] * t)]).T
mat += normal(0.0, 1e-10, size=(dim, 2))
mat = (mat - mean(mat[:-1, :], axis=0)) / std(mat[:-1, :], axis=0)
des_mat = mat.copy()
mat = mult(mat, uniform((2, 2))) + uniform(2)
sfa = mdp.nodes.SFA2Node()
sfa.train(mat)
out = sfa.execute(mat)
assert out.shape[1] == 5, 'Wrong output_dim'
correlation = mult(des_mat[:-1, :].T, numx.take(out[:-1, :], (0, 2), axis=1)) / (dim - 2)
assert_array_almost_equal(abs(correlation), numx.eye(2), decimal - 3)
for nr in xrange(sfa.output_dim):
    qform = sfa.get_quadratic_form(nr)
    outq = qform.apply(mat)
    assert_array_almost_equal(outq, out[:, nr], decimal)
sfa = mdp.nodes.SFANode(output_dim=2)
sfa.train(mat)
out = sfa.execute(mat)
assert out.shape[1] == 2, 'Wrong output_dim'
correlation = mult(des_mat[:-1, :1].T, out[:-1, :1]) / (dim - 2)
assert_array_almost_equal(abs(correlation), numx.eye(1), decimal - 3)
```

## Next Steps


---

*Source: test_SFA2Node.py:3 | Complexity: Advanced | Last updated: 2026-05-18*