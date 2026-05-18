# How To: Nipalsnode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test NIPALSNode

## Prerequisites

**Required Modules:**
- `_tools`
- `test_ICANode`


## Step-by-Step Guide

### Step 1: Assign line_x = numx.zeros(...)

```python
line_x = numx.zeros((1000, 2), 'd')
```

**Verification:**
```python
assert_array_almost_equal(mean(act_mat, axis=0), [0, 0], decimal)
```

### Step 2: Assign line_y = numx.zeros(...)

```python
line_y = numx.zeros((1000, 2), 'd')
```

**Verification:**
```python
assert_array_almost_equal(std(act_mat, axis=0), des_var, decimal)
```

### Step 3: Assign unknown = numx.linspace(...)

```python
line_x[:, 0] = numx.linspace(-1, 1, num=1000, endpoint=1)
```

**Verification:**
```python
assert_array_almost_equal(pca2.d, pca.d, decimal)
```

### Step 4: Assign unknown = numx.linspace(...)

```python
line_y[:, 1] = numx.linspace(-0.2, 0.2, num=1000, endpoint=1)
```

### Step 5: Assign mat = numx.concatenate(...)

```python
mat = numx.concatenate((line_x, line_y))
```

### Step 6: Assign des_var = std(...)

```python
des_var = std(mat, axis=0)
```

### Step 7: Call utils.rotate()

```python
utils.rotate(mat, uniform() * 2 * numx.pi)
```

### Step 8: Assign pca = mdp.nodes.NIPALSNode(...)

```python
pca = mdp.nodes.NIPALSNode(conv=1e-15, max_it=1000)
```

### Step 9: Call pca.train()

```python
pca.train(mat)
```

### Step 10: Assign act_mat = pca.execute(...)

```python
act_mat = pca.execute(mat)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(mean(act_mat, axis=0), [0, 0], decimal)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(std(act_mat, axis=0), des_var, decimal)
```

### Step 13: Call pca.inverse()

```python
pca.inverse(act_mat[:, :1])
```

### Step 14: Assign pca2 = mdp.nodes.PCANode(...)

```python
pca2 = mdp.nodes.PCANode()
```

### Step 15: Call pca2.train()

```python
pca2.train(mat)
```

### Step 16: Call pca2.stop_training()

```python
pca2.stop_training()
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pca2.d, pca.d, decimal)
```


## Complete Example

```python
# Workflow
line_x = numx.zeros((1000, 2), 'd')
line_y = numx.zeros((1000, 2), 'd')
line_x[:, 0] = numx.linspace(-1, 1, num=1000, endpoint=1)
line_y[:, 1] = numx.linspace(-0.2, 0.2, num=1000, endpoint=1)
mat = numx.concatenate((line_x, line_y))
des_var = std(mat, axis=0)
utils.rotate(mat, uniform() * 2 * numx.pi)
mat += uniform(2)
pca = mdp.nodes.NIPALSNode(conv=1e-15, max_it=1000)
pca.train(mat)
act_mat = pca.execute(mat)
assert_array_almost_equal(mean(act_mat, axis=0), [0, 0], decimal)
assert_array_almost_equal(std(act_mat, axis=0), des_var, decimal)
pca.inverse(act_mat[:, :1])
pca2 = mdp.nodes.PCANode()
pca2.train(mat)
pca2.stop_training()
assert_array_almost_equal(pca2.d, pca.d, decimal)
```

## Next Steps


---

*Source: test_contrib.py:67 | Complexity: Advanced | Last updated: 2026-05-18*