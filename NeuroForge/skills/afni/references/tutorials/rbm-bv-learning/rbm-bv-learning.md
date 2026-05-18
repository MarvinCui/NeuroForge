# How To: Rbm Bv Learning

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test RBM bv learning

## Prerequisites

**Required Modules:**
- `mdp`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
I, J = (4, 4)
```

**Verification:**
```python
assert abs(train_bm.bv - bm.bv).max() < 0.5
```

### Step 2: Assign bm = mdp.nodes.RBMNode(...)

```python
bm = mdp.nodes.RBMNode(J, I)
```

### Step 3: Call bm._init_weights()

```python
bm._init_weights()
```

### Step 4: Assign bm.w = numx.eye(...)

```python
bm.w = numx.eye(I, dtype='d')
```

### Step 5: Assign bm.bv = value

```python
bm.bv = numx.linspace(0.1, 0.9, I) * 5
```

### Step 6: Assign data = _generate_data(...)

```python
data = _generate_data(bm, I, 5000)
```

### Step 7: Assign train_bm = mdp.nodes.RBMNode(...)

```python
train_bm = mdp.nodes.RBMNode(J, I)
```

### Step 8: Call train_bm.train()

```python
train_bm.train(data)
```

### Step 9: Assign train_bm.w = numx.eye(...)

```python
train_bm.w = numx.eye(I, dtype='d')
```

### Step 10: Assign N = value

```python
N = data.shape[0]
```

**Verification:**
```python
assert abs(train_bm.bv - bm.bv).max() < 0.5
```

### Step 11: Call train_bm.train()

```python
train_bm.train(data, epsilon=0.6, momentum=0.7)
```

### Step 12: Assign train_bm.w = numx.eye(...)

```python
train_bm.w = numx.eye(I, dtype='d')
```

### Step 13: Call spinner()

```python
spinner()
```


## Complete Example

```python
# Workflow
I, J = (4, 4)
bm = mdp.nodes.RBMNode(J, I)
bm._init_weights()
bm.w = numx.eye(I, dtype='d')
bm.bh *= 0.0
bm.bv = numx.linspace(0.1, 0.9, I) * 5
data = _generate_data(bm, I, 5000)
train_bm = mdp.nodes.RBMNode(J, I)
train_bm.train(data)
train_bm.w = numx.eye(I, dtype='d')
N = data.shape[0]
for k in xrange(5000):
    if k % 5 == 0:
        spinner()
    train_bm.train(data, epsilon=0.6, momentum=0.7)
    if abs(train_bm.bv - bm.bv).max() < 0.5:
        break
    train_bm.w = numx.eye(I, dtype='d')
assert abs(train_bm.bv - bm.bv).max() < 0.5
```

## Next Steps


---

*Source: test_RBM.py:189 | Complexity: Advanced | Last updated: 2026-05-18*