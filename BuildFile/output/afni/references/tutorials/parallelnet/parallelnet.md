# How To: Parallelnet

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test a simple parallel net with big data.

Includes ParallelFlowNode, ParallelCloneLayer, ParallelSFANode
and training via a ParallelFlow.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`
- `mdp.hinet`


## Step-by-Step Guide

### Step 1: 'Test a simple parallel net with big data.\n\n        Includes ParallelFlowNode, ParallelCloneLayer, ParallelSFANode\n        and training via a ParallelFlow.\n        '

```python
'Test a simple parallel net with big data.\n\n        Includes ParallelFlowNode, ParallelCloneLayer, ParallelSFANode\n        and training via a ParallelFlow.\n        '
```

### Step 2: Assign noisenode = mdp.nodes.NormalNoiseNode(...)

```python
noisenode = mdp.nodes.NormalNoiseNode(input_dim=20 * 20, noise_args=(0, 0.0001))
```

### Step 3: Assign sfa_node = mdp.nodes.SFANode(...)

```python
sfa_node = mdp.nodes.SFANode(input_dim=20 * 20, output_dim=10)
```

### Step 4: Assign switchboard = hinet.Rectangular2dSwitchboard(...)

```python
switchboard = hinet.Rectangular2dSwitchboard(in_channels_xy=100, field_channels_xy=20, field_spacing_xy=10)
```

### Step 5: Assign flownode = mdp.hinet.FlowNode(...)

```python
flownode = mdp.hinet.FlowNode(mdp.Flow([noisenode, sfa_node]))
```

### Step 6: Assign sfa_layer = mdp.hinet.CloneLayer(...)

```python
sfa_layer = mdp.hinet.CloneLayer(flownode, switchboard.output_channels)
```

### Step 7: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([switchboard, sfa_layer])
```

### Step 8: Assign data_iterables = value

```python
data_iterables = [None, [n.random.random((10, 100 * 100)) for _ in xrange(3)]]
```

### Step 9: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 10: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```


## Complete Example

```python
# Workflow
'Test a simple parallel net with big data.\n\n        Includes ParallelFlowNode, ParallelCloneLayer, ParallelSFANode\n        and training via a ParallelFlow.\n        '
noisenode = mdp.nodes.NormalNoiseNode(input_dim=20 * 20, noise_args=(0, 0.0001))
sfa_node = mdp.nodes.SFANode(input_dim=20 * 20, output_dim=10)
switchboard = hinet.Rectangular2dSwitchboard(in_channels_xy=100, field_channels_xy=20, field_spacing_xy=10)
flownode = mdp.hinet.FlowNode(mdp.Flow([noisenode, sfa_node]))
sfa_layer = mdp.hinet.CloneLayer(flownode, switchboard.output_channels)
flow = parallel.ParallelFlow([switchboard, sfa_layer])
data_iterables = [None, [n.random.random((10, 100 * 100)) for _ in xrange(3)]]
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
```

## Next Steps


---

*Source: test_parallelhinet.py:55 | Complexity: Advanced | Last updated: 2026-05-18*