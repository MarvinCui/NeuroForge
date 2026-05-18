# How To: Flownode Trainability

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode trainability

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
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2)])
```

**Verification:**
```python
assert flownode.is_trainable() is False
```

### Step 2: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

**Verification:**
```python
assert flownode.is_trainable() is True
```

### Step 3: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=15), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3)])
```

### Step 4: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

**Verification:**
```python
assert flownode.is_trainable() is True
```


## Complete Example

```python
# Workflow
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2)])
flownode = mh.FlowNode(flow)
assert flownode.is_trainable() is False
flow = mdp.Flow([mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=15), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.PCANode(output_dim=3)])
flownode = mh.FlowNode(flow)
assert flownode.is_trainable() is True
```

## Next Steps


---

*Source: test_hinet.py:40 | Complexity: Intermediate | Last updated: 2026-05-18*