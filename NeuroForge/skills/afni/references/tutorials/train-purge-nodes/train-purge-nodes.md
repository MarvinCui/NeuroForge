# How To: Train Purge Nodes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that FlowTrainCallable correctly purges nodes.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test that FlowTrainCallable correctly purges nodes.'

```python
'Test that FlowTrainCallable correctly purges nodes.'
```

**Verification:**
```python
assert flownode._flow[1].__class__.__name__ == '_DummyNode'
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
flownode = mdp.hinet.FlowNode(mdp.Flow([sfa_node, mdp.nodes.IdentityNode(), sfa2_node]))
```

### Step 5: Assign data = n.random.random(...)

```python
data = n.random.random((30, 10))
```

### Step 6: Call mdp.activate_extension()

```python
mdp.activate_extension('parallel')
```

**Verification:**
```python
assert flownode._flow[1].__class__.__name__ == '_DummyNode'
```

### Step 7: Assign clbl = mdp.parallel.FlowTrainCallable(...)

```python
clbl = mdp.parallel.FlowTrainCallable(flownode)
```

### Step 8: Assign flownode = clbl(...)

```python
flownode = clbl(data)
```

### Step 9: Call mdp.deactivate_extension()

```python
mdp.deactivate_extension('parallel')
```


## Complete Example

```python
# Workflow
'Test that FlowTrainCallable correctly purges nodes.'
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
flownode = mdp.hinet.FlowNode(mdp.Flow([sfa_node, mdp.nodes.IdentityNode(), sfa2_node]))
data = n.random.random((30, 10))
mdp.activate_extension('parallel')
try:
    clbl = mdp.parallel.FlowTrainCallable(flownode)
    flownode = clbl(data)
finally:
    mdp.deactivate_extension('parallel')
assert flownode._flow[1].__class__.__name__ == '_DummyNode'
```

## Next Steps


---

*Source: test_parallelflows.py:192 | Complexity: Advanced | Last updated: 2026-05-18*