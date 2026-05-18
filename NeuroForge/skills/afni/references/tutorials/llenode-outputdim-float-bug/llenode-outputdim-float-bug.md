# How To: Llenode Outputdim Float Bug

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LLENode outputdim float bug

## Prerequisites

**Required Modules:**
- `_tools`
- `test_ICANode`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
n, k = (50, 2)
```

**Verification:**
```python
assert err.max() == 0
```

### Step 2: Assign unknown = _s_shape_1D(...)

```python
x, y, z, t = _s_shape_1D(n)
```

### Step 3: Assign data = value

```python
data = numx.asarray([x, y, z]).T
```

### Step 4: Assign res = mdp.nodes.LLENode(...)

```python
res = mdp.nodes.LLENode(k, output_dim=0.9, svd=True)(data)
```

### Step 5: Assign err = _compare_neighbors(...)

```python
err = _compare_neighbors(data, res, k)
```

**Verification:**
```python
assert err.max() == 0
```


## Complete Example

```python
# Workflow
n, k = (50, 2)
x, y, z, t = _s_shape_1D(n)
data = numx.asarray([x, y, z]).T
res = mdp.nodes.LLENode(k, output_dim=0.9, svd=True)(data)
err = _compare_neighbors(data, res, k)
assert err.max() == 0
```

## Next Steps


---

*Source: test_contrib.py:150 | Complexity: Intermediate | Last updated: 2026-05-18*