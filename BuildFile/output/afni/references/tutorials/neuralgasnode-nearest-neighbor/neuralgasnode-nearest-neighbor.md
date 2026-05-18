# How To: Neuralgasnode Nearest Neighbor

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test NeuralGasNode nearest neighbor

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign start_poss = value

```python
start_poss = [numx.asarray([2.0, 0]), numx.asarray([-2.0, 0])]
```

**Verification:**
```python
assert_almost_equal(dists[0], 1.0, 7)
```

### Step 2: Assign ng = mdp.nodes.NeuralGasNode(...)

```python
ng = mdp.nodes.NeuralGasNode(start_poss=start_poss, max_epochs=4)
```

**Verification:**
```python
assert_almost_equal(nodes[0].data.pos, numx.asarray([2.0, 0.0]), 7)
```

### Step 3: Assign x = numx.asarray(...)

```python
x = numx.asarray([[2.0, 0]])
```

### Step 4: Call ng.train()

```python
ng.train(x)
```

### Step 5: Assign unknown = ng.nearest_neighbor(...)

```python
nodes, dists = ng.nearest_neighbor(numx.asarray([[3.0, 0]]))
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(dists[0], 1.0, 7)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(nodes[0].data.pos, numx.asarray([2.0, 0.0]), 7)
```


## Complete Example

```python
# Workflow
start_poss = [numx.asarray([2.0, 0]), numx.asarray([-2.0, 0])]
ng = mdp.nodes.NeuralGasNode(start_poss=start_poss, max_epochs=4)
x = numx.asarray([[2.0, 0]])
ng.train(x)
nodes, dists = ng.nearest_neighbor(numx.asarray([[3.0, 0]]))
assert_almost_equal(dists[0], 1.0, 7)
assert_almost_equal(nodes[0].data.pos, numx.asarray([2.0, 0.0]), 7)
```

## Next Steps


---

*Source: test_NeuralGasNode.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*