# How To: Layer

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Simple random test with three nodes.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`
- `mdp.hinet`


## Step-by-Step Guide

### Step 1: 'Test Simple random test with three nodes.'

```python
'Test Simple random test with three nodes.'
```

### Step 2: Assign node1 = mdp.nodes.SFANode(...)

```python
node1 = mdp.nodes.SFANode(input_dim=10, output_dim=5)
```

### Step 3: Assign node2 = mdp.nodes.SFANode(...)

```python
node2 = mdp.nodes.SFANode(input_dim=17, output_dim=3)
```

### Step 4: Assign node3 = mdp.nodes.SFANode(...)

```python
node3 = mdp.nodes.SFANode(input_dim=3, output_dim=1)
```

### Step 5: Assign layer = mdp.hinet.Layer(...)

```python
layer = mdp.hinet.Layer([node1, node2, node3])
```

### Step 6: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([layer])
```

### Step 7: Assign data_iterables = value

```python
data_iterables = [[n.random.random((10, 30)) for _ in xrange(3)]]
```

### Step 8: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 9: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```


## Complete Example

```python
# Workflow
'Test Simple random test with three nodes.'
node1 = mdp.nodes.SFANode(input_dim=10, output_dim=5)
node2 = mdp.nodes.SFANode(input_dim=17, output_dim=3)
node3 = mdp.nodes.SFANode(input_dim=3, output_dim=1)
layer = mdp.hinet.Layer([node1, node2, node3])
flow = parallel.ParallelFlow([layer])
data_iterables = [[n.random.random((10, 30)) for _ in xrange(3)]]
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
```

## Next Steps


---

*Source: test_parallelhinet.py:76 | Complexity: Advanced | Last updated: 2026-05-18*