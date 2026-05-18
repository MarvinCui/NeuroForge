# How To: Node Copy With Arrays And Subnodes

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Node copy with arrays and subnodes

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `cPickle`
- `mdp`
- `_tools`
- `py.test`


## Step-by-Step Guide

### Step 1: Assign node = mdp.Node(...)

```python
node = mdp.Node()
```

**Verification:**
```python
assert hasattr(node2, 'node')
```

### Step 2: Assign node.node = mdp.Node(...)

```python
node.node = mdp.Node()
```

**Verification:**
```python
assert mdp.numx.all(node2.node.x == node.node.x)
```

### Step 3: Assign node.node.x = mdp.numx.zeros(...)

```python
node.node.x = mdp.numx.zeros((2, 2))
```

### Step 4: Assign node2 = node.copy(...)

```python
node2 = node.copy()
```

**Verification:**
```python
assert hasattr(node2, 'node')
```


## Complete Example

```python
# Workflow
node = mdp.Node()
node.node = mdp.Node()
node.node.x = mdp.numx.zeros((2, 2))
node2 = node.copy()
assert hasattr(node2, 'node')
assert mdp.numx.all(node2.node.x == node.node.x)
```

## Next Steps


---

*Source: test_node_operations.py:23 | Complexity: Intermediate | Last updated: 2026-05-18*