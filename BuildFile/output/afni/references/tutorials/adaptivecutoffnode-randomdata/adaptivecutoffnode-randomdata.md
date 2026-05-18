# How To: Adaptivecutoffnode Randomdata

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test AdaptiveCutoffNode on a large random data.

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test AdaptiveCutoffNode on a large random data.'

```python
'Test AdaptiveCutoffNode on a large random data.'
```

### Step 2: Assign node = mdp.nodes.AdaptiveCutoffNode(...)

```python
node = mdp.nodes.AdaptiveCutoffNode(lower_cutoff_fraction=0.2, upper_cutoff_fraction=0.4, hist_fraction=0.5)
```

### Step 3: Assign x1 = numx_rand.random(...)

```python
x1 = numx_rand.random((1000, 3))
```

### Step 4: Assign x2 = numx_rand.random(...)

```python
x2 = numx_rand.random((500, 3))
```

### Step 5: Assign x = numx.concatenate(...)

```python
x = numx.concatenate([x1, x2])
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

### Step 9: Call node.execute()

```python
node.execute(x)
```


## Complete Example

```python
# Workflow
'Test AdaptiveCutoffNode on a large random data.'
node = mdp.nodes.AdaptiveCutoffNode(lower_cutoff_fraction=0.2, upper_cutoff_fraction=0.4, hist_fraction=0.5)
x1 = numx_rand.random((1000, 3))
x2 = numx_rand.random((500, 3))
x = numx.concatenate([x1, x2])
node.train(x1)
node.train(x2)
node.stop_training()
node.execute(x)
```

## Next Steps


---

*Source: test_AdaptiveCutoffNode.py:25 | Complexity: Advanced | Last updated: 2026-05-18*