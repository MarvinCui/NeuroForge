# How To: Flownode Forksingle

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that ParallelFlowNode forks only the first training node.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`
- `mdp.hinet`


## Step-by-Step Guide

### Step 1: 'Test that ParallelFlowNode forks only the first training node.'

```python
'Test that ParallelFlowNode forks only the first training node.'
```

**Verification:**
```python
assert flownode._flow[0] is not forked_flownode._flow[0]
```

### Step 2: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=3)])
```

**Verification:**
```python
assert flownode._flow[1] is forked_flownode._flow[1]
```

### Step 3: Assign flownode = mdp.hinet.FlowNode(...)

```python
flownode = mdp.hinet.FlowNode(flow)
```

**Verification:**
```python
assert flownode._flow[2] is forked_flownode._flow[2]
```

### Step 4: Assign forked_flownode = flownode.fork(...)

```python
forked_flownode = flownode.fork()
```

**Verification:**
```python
assert flownode._flow[0] is not forked_flownode._flow[0]
```

### Step 5: Assign unknown._cov_mtx = None

```python
flownode._flow[2]._cov_mtx = None
```

### Step 6: Call flownode.join()

```python
flownode.join(forked_flownode)
```


## Complete Example

```python
# Workflow
'Test that ParallelFlowNode forks only the first training node.'
flow = mdp.Flow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=2), mdp.nodes.SFANode(output_dim=3)])
flownode = mdp.hinet.FlowNode(flow)
forked_flownode = flownode.fork()
assert flownode._flow[0] is not forked_flownode._flow[0]
assert flownode._flow[1] is forked_flownode._flow[1]
assert flownode._flow[2] is forked_flownode._flow[2]
flownode._flow[2]._cov_mtx = None
flownode.join(forked_flownode)
```

## Next Steps


---

*Source: test_parallelhinet.py:40 | Complexity: Intermediate | Last updated: 2026-05-18*