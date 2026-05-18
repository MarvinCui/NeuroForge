# How To: Rbm Stability

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test RBM stability

## Prerequisites

**Required Modules:**
- `mdp`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
I, J = (8, 2)
```

**Verification:**
```python
assert_array_almost_equal(real_w, bm.w, 1)
```

### Step 2: Assign bm = mdp.nodes.RBMNode(...)

```python
bm = mdp.nodes.RBMNode(J, I)
```

**Verification:**
```python
assert_array_almost_equal(real_bv, bm.bv, 1)
```

### Step 3: Call bm._init_weights()

```python
bm._init_weights()
```

**Verification:**
```python
assert_array_almost_equal(real_bh, bm.bh, 1)
```

### Step 4: Assign bm.w = value

```python
bm.w = mdp.utils.random_rot(max(I, J), dtype='d')[:I, :J]
```

### Step 5: Assign bm.bv = numx_rand.randn(...)

```python
bm.bv = numx_rand.randn(I)
```

### Step 6: Assign bm.bh = numx_rand.randn(...)

```python
bm.bh = numx_rand.randn(J)
```

### Step 7: Assign real_w = bm.w.copy(...)

```python
real_w = bm.w.copy()
```

### Step 8: Assign real_bv = bm.bv.copy(...)

```python
real_bv = bm.bv.copy()
```

### Step 9: Assign real_bh = bm.bh.copy(...)

```python
real_bh = bm.bh.copy()
```

### Step 10: Assign N = 10000.0

```python
N = 10000.0
```

### Step 11: Assign v = numx_rand.randint.astype(...)

```python
v = numx_rand.randint(0, 2, (N, I)).astype('d')
```

### Step 12: Call bm.stop_training()

```python
bm.stop_training()
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(real_w, bm.w, 1)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(real_bv, bm.bv, 1)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(real_bh, bm.bh, 1)
```

### Step 16: Assign unknown = bm._sample_h(...)

```python
p, h = bm._sample_h(v)
```

### Step 17: Assign unknown = bm._sample_v(...)

```python
p, v = bm._sample_v(h)
```

### Step 18: Call bm.train()

```python
bm.train(v)
```

### Step 19: Call spinner()

```python
spinner()
```

### Step 20: Call spinner()

```python
spinner()
```


## Complete Example

```python
# Workflow
I, J = (8, 2)
bm = mdp.nodes.RBMNode(J, I)
bm._init_weights()
bm.w = mdp.utils.random_rot(max(I, J), dtype='d')[:I, :J]
bm.bv = numx_rand.randn(I)
bm.bh = numx_rand.randn(J)
real_w = bm.w.copy()
real_bv = bm.bv.copy()
real_bh = bm.bh.copy()
N = 10000.0
v = numx_rand.randint(0, 2, (N, I)).astype('d')
for k in xrange(100):
    if k % 5 == 0:
        spinner()
    p, h = bm._sample_h(v)
    p, v = bm._sample_v(h)
for k in xrange(100):
    if k % 5 == 0:
        spinner()
    bm.train(v)
bm.stop_training()
assert_array_almost_equal(real_w, bm.w, 1)
assert_array_almost_equal(real_bv, bm.bv, 1)
assert_array_almost_equal(real_bh, bm.bh, 1)
```

## Next Steps


---

*Source: test_RBM.py:114 | Complexity: Advanced | Last updated: 2026-05-18*