# How To: Flownode Copy1

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FlowNode copy1

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
flow = mdp.Flow([mdp.nodes.PCANode(), mdp.nodes.SFANode()])
```

### Step 2: Assign flownode = mh.FlowNode(...)

```python
flownode = mh.FlowNode(flow)
```

### Step 3: Call flownode.copy()

```python
flownode.copy()
```


## Complete Example

```python
# Workflow
flow = mdp.Flow([mdp.nodes.PCANode(), mdp.nodes.SFANode()])
flownode = mh.FlowNode(flow)
flownode.copy()
```

## Next Steps


---

*Source: test_hinet.py:124 | Complexity: Beginner | Last updated: 2026-05-18*