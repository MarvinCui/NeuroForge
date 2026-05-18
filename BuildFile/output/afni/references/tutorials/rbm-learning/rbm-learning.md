# How To: Rbm Learning

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test RBM learning

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
assert bm._train_err / N < 0.1
```

### Step 2: Assign bm = mdp.nodes.RBMNode(...)

```python
bm = mdp.nodes.RBMNode(J, I)
```

### Step 3: Assign bm.w = value

```python
bm.w = mdp.utils.random_rot(max(I, J), dtype='d')[:I, :J]
```

### Step 4: Assign N = 10000.0

```python
N = 10000.0
```

### Step 5: Assign v = numx.zeros(...)

```python
v = numx.zeros((N, I))
```

**Verification:**
```python
assert bm._train_err / N < 0.1
```

### Step 6: Assign r = numx_rand.random(...)

```python
r = numx_rand.random()
```

### Step 7: Call bm.train()

```python
bm.train(v, epsilon=0.3, momentum=mom)
```

### Step 8: Assign unknown = value

```python
v[n, :] = [0, 1, 0, 1]
```

### Step 9: Call spinner()

```python
spinner()
```

### Step 10: Assign mom = 0.9

```python
mom = 0.9
```

### Step 11: Assign mom = 0.5

```python
mom = 0.5
```

### Step 12: Assign unknown = value

```python
v[n, :] = [1, 0, 1, 0]
```


## Complete Example

```python
# Workflow
I, J = (4, 2)
bm = mdp.nodes.RBMNode(J, I)
bm.w = mdp.utils.random_rot(max(I, J), dtype='d')[:I, :J]
N = 10000.0
v = numx.zeros((N, I))
for n in xrange(int(N)):
    r = numx_rand.random()
    if r > 0.666:
        v[n, :] = [0, 1, 0, 1]
    elif r > 0.333:
        v[n, :] = [1, 0, 1, 0]
for k in xrange(1500):
    if k % 5 == 0:
        spinner()
    if k > 5:
        mom = 0.9
    else:
        mom = 0.5
    bm.train(v, epsilon=0.3, momentum=mom)
    if bm._train_err / N < 0.1:
        break
assert bm._train_err / N < 0.1
```

## Next Steps


---

*Source: test_RBM.py:149 | Complexity: Advanced | Last updated: 2026-05-18*