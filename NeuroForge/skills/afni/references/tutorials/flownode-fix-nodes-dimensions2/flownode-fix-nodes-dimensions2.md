# How To: Flownode Fix Nodes Dimensions2

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode fix nodes dimensions2

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
flow = mdp.Flow([mdp.nodes.IdentityNode(), mdp.nodes.IdentityNode()])
```

**Verification:**
```python
assert flownode.output_dim == 10
```

### Step 2: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 3: Call py.test.raises()

```python
py.test.raises(mdp.InconsistentDimException, lambda: flownode.set_output_dim(10))
```

### Step 4: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([100, 10])
```

### Step 5: Call flownode.execute()

```python
flownode.execute(x)
```

**Verification:**
```python
assert flownode.output_dim == 10
```


## Complete Example

```python
# Workflow
flow = mdp.Flow([mdp.nodes.IdentityNode(), mdp.nodes.IdentityNode()])
flownode = mh.FlowNode(flow)
py.test.raises(mdp.InconsistentDimException, lambda: flownode.set_output_dim(10))
x = numx_rand.random([100, 10])
flownode.execute(x)
assert flownode.output_dim == 10
```

## Next Steps


---

*Source: test_hinet.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*