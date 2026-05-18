# How To: Flownode Fix Nodes Dimensions1

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode fix nodes dimensions1

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

**Verification:**
```python
assert flownode.output_dim == 3
```

### Step 2: Assign last_node = mdp.nodes.IdentityNode(...)

```python
last_node = mdp.nodes.IdentityNode()
```

**Verification:**
```python
assert last_node.input_dim == 3
```

### Step 3: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.PCANode(output_dim=3), mdp.nodes.IdentityNode(), last_node])
```

**Verification:**
```python
assert last_node.output_dim == 3
```

### Step 4: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 5: Call flownode.train()

```python
flownode.train(x)
```

### Step 6: Call flownode.stop_training()

```python
flownode.stop_training()
```

**Verification:**
```python
assert flownode.output_dim == 3
```


## Complete Example

```python
# Workflow
x = numx_rand.random([100, 10])
last_node = mdp.nodes.IdentityNode()
flow = mdp.Flow([mdp.nodes.PCANode(output_dim=3), mdp.nodes.IdentityNode(), last_node])
flownode = mh.FlowNode(flow)
flownode.train(x)
flownode.stop_training()
assert flownode.output_dim == 3
assert last_node.input_dim == 3
assert last_node.output_dim == 3
```

## Next Steps


---

*Source: test_hinet.py:75 | Complexity: Intermediate | Last updated: 2026-05-18*