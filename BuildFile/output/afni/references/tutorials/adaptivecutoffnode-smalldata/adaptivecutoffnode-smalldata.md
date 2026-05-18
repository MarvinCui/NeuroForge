# How To: Adaptivecutoffnode Smalldata

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test AdaptiveCutoffNode thoroughly on a small data set.

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test AdaptiveCutoffNode thoroughly on a small data set.'

```python
'Test AdaptiveCutoffNode thoroughly on a small data set.'
```

**Verification:**
```python
assert numx.all(x == node.data_hist)
```

### Step 2: Assign x1 = numx.array(...)

```python
x1 = numx.array([[0.1, 0.3], [0.3, 0.5], [0.5, 0.7]])
```

**Verification:**
```python
assert numx.all(node.lower_bounds == numx.array([0.2, 0.3]))
```

### Step 3: Assign x2 = numx.array(...)

```python
x2 = numx.array([[0.4, 0.6], [0.2, 0.4], [0.6, 0.2]])
```

**Verification:**
```python
assert numx.all(node.upper_bounds == numx.array([0.4, 0.5]))
```

### Step 4: Assign x = numx.concatenate(...)

```python
x = numx.concatenate([x1, x2])
```

**Verification:**
```python
assert (x_clip == x_goal).all()
```

### Step 5: Assign node = mdp.nodes.AdaptiveCutoffNode(...)

```python
node = mdp.nodes.AdaptiveCutoffNode(lower_cutoff_fraction=0.2, upper_cutoff_fraction=0.4)
```

### Step 6: Call node.train()

```python
node.train(x1)
```

### Step 7: Call node.train()

```python
node.train(x2)
```

### Step 8: Call node.stop_training()

```python
node.stop_training()
```

**Verification:**
```python
assert numx.all(x == node.data_hist)
```

### Step 9: Assign x_test = numx.array(...)

```python
x_test = numx.array([[0.1, 0.2], [0.3, 0.4], [0.5, 0.6]])
```

### Step 10: Assign x_clip = node.execute(...)

```python
x_clip = node.execute(x_test)
```

### Step 11: Assign x_goal = numx.array(...)

```python
x_goal = numx.array([[0.2, 0.3], [0.3, 0.4], [0.4, 0.5]])
```

**Verification:**
```python
assert (x_clip == x_goal).all()
```


## Complete Example

```python
# Workflow
'Test AdaptiveCutoffNode thoroughly on a small data set.'
x1 = numx.array([[0.1, 0.3], [0.3, 0.5], [0.5, 0.7]])
x2 = numx.array([[0.4, 0.6], [0.2, 0.4], [0.6, 0.2]])
x = numx.concatenate([x1, x2])
node = mdp.nodes.AdaptiveCutoffNode(lower_cutoff_fraction=0.2, upper_cutoff_fraction=0.4)
node.train(x1)
node.train(x2)
node.stop_training()
assert numx.all(x == node.data_hist)
assert numx.all(node.lower_bounds == numx.array([0.2, 0.3]))
assert numx.all(node.upper_bounds == numx.array([0.4, 0.5]))
x_test = numx.array([[0.1, 0.2], [0.3, 0.4], [0.5, 0.6]])
x_clip = node.execute(x_test)
x_goal = numx.array([[0.2, 0.3], [0.3, 0.4], [0.4, 0.5]])
assert (x_clip == x_goal).all()
```

## Next Steps


---

*Source: test_AdaptiveCutoffNode.py:4 | Complexity: Advanced | Last updated: 2026-05-18*