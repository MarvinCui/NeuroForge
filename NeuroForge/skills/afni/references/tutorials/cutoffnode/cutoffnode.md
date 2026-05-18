# How To: Cutoffnode

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test CutoffNode

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign node = mdp.nodes.CutoffNode(...)

```python
node = mdp.nodes.CutoffNode(-1.5, 1.2)
```

**Verification:**
```python
assert numx.all(y == y_ref)
```

### Step 2: Assign x = numx.array(...)

```python
x = numx.array([[0.1, 0, -2, 3, 1.2, -1.5, -3.33]])
```

### Step 3: Assign y_ref = numx.array(...)

```python
y_ref = numx.array([[0.1, 0, -1.5, 1.2, 1.2, -1.5, -1.5]])
```

### Step 4: Assign y = node.execute(...)

```python
y = node.execute(x)
```

**Verification:**
```python
assert numx.all(y == y_ref)
```


## Complete Example

```python
# Workflow
node = mdp.nodes.CutoffNode(-1.5, 1.2)
x = numx.array([[0.1, 0, -2, 3, 1.2, -1.5, -3.33]])
y_ref = numx.array([[0.1, 0, -1.5, 1.2, 1.2, -1.5, -1.5]])
y = node.execute(x)
assert numx.all(y == y_ref)
```

## Next Steps


---

*Source: test_CutoffNode.py:3 | Complexity: Intermediate | Last updated: 2026-05-18*