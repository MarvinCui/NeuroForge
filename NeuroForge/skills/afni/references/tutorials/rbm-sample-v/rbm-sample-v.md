# How To: Rbm Sample V

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test RBM sample v

## Prerequisites

**Required Modules:**
- `mdp`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
I, J = (4, 2)
```

**Verification:**
```python
assert_array_almost_equal(prob, expected_probs, 8)
```

### Step 2: Assign bm = mdp.nodes.RBMNode(...)

```python
bm = mdp.nodes.RBMNode(J, I)
```

**Verification:**
```python
assert_array_almost_equal(distr, expected_probs[n, :], 1)
```

### Step 3: Call bm.train()

```python
bm.train(numx.zeros((1, I)))
```

**Verification:**
```python
assert_array_almost_equal(prob, expected_probs, 8)
```

### Step 4: Assign unknown = value

```python
bm.w[:, 0] = [1, 0, 1, 0]
```

**Verification:**
```python
assert_array_almost_equal(distr, expected_probs[n, :], 1)
```

### Step 5: Assign unknown = value

```python
bm.w[:, 1] = [0, 1, 0, 1]
```

### Step 6: Assign h = numx.array(...)

```python
h = numx.array([[0, 0], [1, 0], [0, 1], [1, 1.0]])
```

### Step 7: Assign v = value

```python
v = []
```

### Step 8: Assign expected_probs = numx.array(...)

```python
expected_probs = numx.array([[0.5, 0.5, 0.5, 0.5], [1.0, 0.5, 1.0, 0.5], [0.5, 1.0, 0.5, 1.0], [1.0, 1.0, 1.0, 1.0]])
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(prob, expected_probs, 8)
```

### Step 10: Assign v = numx.array(...)

```python
v = numx.array(v)
```

### Step 11: Assign v = value

```python
v = []
```

### Step 12: Assign expected_probs = numx.array(...)

```python
expected_probs = numx.array([[0.0, 0.0, 0.0, 0.0], [1.0, 0.0, 1.0, 0.0], [0.0, 1.0, 0.0, 1.0], [1.0, 1.0, 1.0, 1.0]])
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(prob, expected_probs, 8)
```

### Step 14: Assign v = numx.array(...)

```python
v = numx.array(v)
```

### Step 15: Assign unknown = bm.sample_v(...)

```python
prob, sample = bm.sample_v(h)
```

### Step 16: Call v.append()

```python
v.append(sample)
```

### Step 17: Assign distr = unknown.mean(...)

```python
distr = v[:, n, :].mean(axis=0)
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(distr, expected_probs[n, :], 1)
```

### Step 19: Assign unknown = bm.sample_v(...)

```python
prob, sample = bm.sample_v(h)
```

### Step 20: Call v.append()

```python
v.append(sample)
```

### Step 21: Assign distr = unknown.mean(...)

```python
distr = v[:, n, :].mean(axis=0)
```

### Step 22: Call assert_array_almost_equal()

```python
assert_array_almost_equal(distr, expected_probs[n, :], 1)
```


## Complete Example

```python
# Workflow
I, J = (4, 2)
bm = mdp.nodes.RBMNode(J, I)
bm.train(numx.zeros((1, I)))
bm.w[:, 0] = [1, 0, 1, 0]
bm.w[:, 1] = [0, 1, 0, 1]
bm.w *= 20000.0
bm.bv *= 0
bm.bh *= 0
h = numx.array([[0, 0], [1, 0], [0, 1], [1, 1.0]])
v = []
for n in xrange(1000):
    prob, sample = bm.sample_v(h)
    v.append(sample)
expected_probs = numx.array([[0.5, 0.5, 0.5, 0.5], [1.0, 0.5, 1.0, 0.5], [0.5, 1.0, 0.5, 1.0], [1.0, 1.0, 1.0, 1.0]])
assert_array_almost_equal(prob, expected_probs, 8)
v = numx.array(v)
for n in xrange(4):
    distr = v[:, n, :].mean(axis=0)
    assert_array_almost_equal(distr, expected_probs[n, :], 1)
bm.bv -= 100.0
v = []
for n in xrange(1000):
    prob, sample = bm.sample_v(h)
    v.append(sample)
expected_probs = numx.array([[0.0, 0.0, 0.0, 0.0], [1.0, 0.0, 1.0, 0.0], [0.0, 1.0, 0.0, 1.0], [1.0, 1.0, 1.0, 1.0]])
assert_array_almost_equal(prob, expected_probs, 8)
v = numx.array(v)
for n in xrange(4):
    distr = v[:, n, :].mean(axis=0)
    assert_array_almost_equal(distr, expected_probs[n, :], 1)
```

## Next Steps


---

*Source: test_RBM.py:59 | Complexity: Advanced | Last updated: 2026-05-18*