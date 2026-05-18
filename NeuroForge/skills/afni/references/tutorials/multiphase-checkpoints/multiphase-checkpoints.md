# How To: Multiphase Checkpoints

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parallel checkpoint flow.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test parallel checkpoint flow.'

```python
'Test parallel checkpoint flow.'
```

### Step 2: Assign sfa_node = mdp.nodes.SFANode(...)

```python
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
```

### Step 3: Assign sfa2_node = mdp.nodes.SFA2Node(...)

```python
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
```

### Step 4: Assign flownode = mdp.hinet.FlowNode(...)

```python
flownode = mdp.hinet.FlowNode(mdp.Flow([sfa_node, sfa2_node]))
```

### Step 5: Assign flow = parallel.ParallelCheckpointFlow(...)

```python
flow = parallel.ParallelCheckpointFlow([flownode, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=5)])
```

### Step 6: Assign data_iterables = value

```python
data_iterables = [[n.random.random((30, 10)) for _ in xrange(6)], None, [n.random.random((30, 10)) for _ in xrange(6)]]
```

### Step 7: Assign checkpoint = mdp.CheckpointFunction(...)

```python
checkpoint = mdp.CheckpointFunction()
```

### Step 8: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 9: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler, checkpoints=checkpoint)
```


## Complete Example

```python
# Workflow
'Test parallel checkpoint flow.'
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
flownode = mdp.hinet.FlowNode(mdp.Flow([sfa_node, sfa2_node]))
flow = parallel.ParallelCheckpointFlow([flownode, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=5)])
data_iterables = [[n.random.random((30, 10)) for _ in xrange(6)], None, [n.random.random((30, 10)) for _ in xrange(6)]]
checkpoint = mdp.CheckpointFunction()
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler, checkpoints=checkpoint)
```

## Next Steps


---

*Source: test_parallelflows.py:111 | Complexity: Advanced | Last updated: 2026-05-18*