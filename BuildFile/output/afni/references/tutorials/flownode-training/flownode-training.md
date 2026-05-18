# How To: Flownode Training

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode training

## Prerequisites

**Required Modules:**
- `__future__`
- `py.test`
- `StringIO`
- `mdp.hinet`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=15, reduce=True), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3, reduce=True)])
```

### Step 2: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 3: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([300, 20])
```

### Step 4: Call flownode.execute()

```python
flownode.execute(x)
```

### Step 5: Call flownode.train()

```python
flownode.train(x)
```

### Step 6: Call flownode.stop_training()

```python
flownode.stop_training()
```


## Complete Example

```python
# Workflow
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=15, reduce=True), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3, reduce=True)])
flownode = mh.FlowNode(flow)
x = numx_rand.random([300, 20])
while flownode.get_remaining_train_phase() > 0:
    flownode.train(x)
    flownode.stop_training()
flownode.execute(x)
```

## Next Steps


---

*Source: test_hinet.py:28 | Complexity: Intermediate | Last updated: 2026-05-18*