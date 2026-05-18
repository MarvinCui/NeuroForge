# How To: Flownode Pretrained Node

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode pretrained node

## Prerequisites

**Required Modules:**
- `__future__`
- `py.test`
- `StringIO`
- `mdp.hinet`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([100, 10])
```

### Step 2: Assign pretrained_node = mdp.nodes.PCANode(...)

```python
pretrained_node = mdp.nodes.PCANode(output_dim=6)
```

### Step 3: Call pretrained_node.train()

```python
pretrained_node.train(x)
```

### Step 4: Call pretrained_node.stop_training()

```python
pretrained_node.stop_training()
```

### Step 5: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([pretrained_node, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3)])
```

### Step 6: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 7: Call flownode.execute()

```python
flownode.execute(x)
```

### Step 8: Call flownode.train()

```python
flownode.train(x)
```

### Step 9: Call flownode.stop_training()

```python
flownode.stop_training()
```


## Complete Example

```python
# Workflow
x = numx_rand.random([100, 10])
pretrained_node = mdp.nodes.PCANode(output_dim=6)
pretrained_node.train(x)
pretrained_node.stop_training()
flow = mdp.Flow([pretrained_node, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3)])
flownode = mh.FlowNode(flow)
while flownode.get_remaining_train_phase() > 0:
    flownode.train(x)
    flownode.stop_training()
flownode.execute(x)
```

## Next Steps


---

*Source: test_hinet.py:61 | Complexity: Advanced | Last updated: 2026-05-18*