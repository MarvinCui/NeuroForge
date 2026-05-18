# How To: Flownode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ParallelFlowNode.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`
- `mdp.hinet`


## Step-by-Step Guide

### Step 1: 'Test ParallelFlowNode.'

```python
'Test ParallelFlowNode.'
```

### Step 2: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=3)])
```

### Step 3: Assign flownode = mdp.hinet.FlowNode(...)

```python
flownode = mdp.hinet.FlowNode(flow)
```

### Step 4: Assign x = n.random.random(...)

```python
x = n.random.random([100, 50])
```

### Step 5: Assign chunksize = 25

```python
chunksize = 25
```

### Step 6: Assign chunks = value

```python
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
```

### Step 7: Call flownode.execute()

```python
flownode.execute(x)
```

### Step 8: Call flownode.stop_training()

```python
flownode.stop_training()
```

### Step 9: Assign forked_node = flownode.fork(...)

```python
forked_node = flownode.fork()
```

### Step 10: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 11: Call flownode.join()

```python
flownode.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test ParallelFlowNode.'
flow = mdp.Flow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=3)])
flownode = mdp.hinet.FlowNode(flow)
x = n.random.random([100, 50])
chunksize = 25
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
while flownode.get_remaining_train_phase() > 0:
    for chunk in chunks:
        forked_node = flownode.fork()
        forked_node.train(chunk)
        flownode.join(forked_node)
    flownode.stop_training()
flownode.execute(x)
```

## Next Steps


---

*Source: test_parallelhinet.py:21 | Complexity: Advanced | Last updated: 2026-05-18*