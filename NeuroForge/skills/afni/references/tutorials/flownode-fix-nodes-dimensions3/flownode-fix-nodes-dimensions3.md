# How To: Flownode Fix Nodes Dimensions3

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode fix nodes dimensions3

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
flow = mdp.Flow([mdp.nodes.IdentityNode()])
```

### Step 2: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 3: Call flownode.set_output_dim()

```python
flownode.set_output_dim(10)
```

### Step 4: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([100, 10])
```

### Step 5: Call flownode.execute()

```python
flownode.execute(x)
```


## Complete Example

```python
# Workflow
flow = mdp.Flow([mdp.nodes.IdentityNode()])
flownode = mh.FlowNode(flow)
flownode.set_output_dim(10)
x = numx_rand.random([100, 10])
flownode.execute(x)
```

## Next Steps


---

*Source: test_hinet.py:101 | Complexity: Intermediate | Last updated: 2026-05-18*