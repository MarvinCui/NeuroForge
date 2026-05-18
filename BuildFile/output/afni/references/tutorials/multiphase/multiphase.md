# How To: Multiphase

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parallel training and execution for nodes with multiple
training phases.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test parallel training and execution for nodes with multiple\n    training phases.\n    '

```python
'Test parallel training and execution for nodes with multiple\n    training phases.\n    '
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

### Step 5: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([flownode, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=5)])
```

### Step 6: Assign data_iterables = value

```python
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], None, [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
```

### Step 7: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 8: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```

### Step 9: Assign x = n.random.random(...)

```python
x = n.random.random([100, 10])
```

### Step 10: Call flow.execute()

```python
flow.execute(x)
```

### Step 11: Assign iterable = value

```python
iterable = [n.random.random((20, 10)) for _ in xrange(6)]
```

### Step 12: Call flow.execute()

```python
flow.execute(iterable, scheduler=scheduler)
```


## Complete Example

```python
# Workflow
'Test parallel training and execution for nodes with multiple\n    training phases.\n    '
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
flownode = mdp.hinet.FlowNode(mdp.Flow([sfa_node, sfa2_node]))
flow = parallel.ParallelFlow([flownode, mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=5)])
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], None, [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
x = n.random.random([100, 10])
flow.execute(x)
iterable = [n.random.random((20, 10)) for _ in xrange(6)]
flow.execute(iterable, scheduler=scheduler)
```

## Next Steps


---

*Source: test_parallelflows.py:73 | Complexity: Advanced | Last updated: 2026-05-18*