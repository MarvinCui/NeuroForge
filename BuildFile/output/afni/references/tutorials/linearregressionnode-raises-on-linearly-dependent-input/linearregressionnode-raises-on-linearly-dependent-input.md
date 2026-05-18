# How To: Linearregressionnode Raises On Linearly Dependent Input

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LinearRegressionNode raises on linearly dependent input

## Prerequisites

**Required Modules:**
- `py.test`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign beta = numx_rand.uniform(...)

```python
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
```

### Step 2: Assign x = numx.linspace(...)

```python
x = numx.linspace(-20, 20, TLEN)
```

### Step 3: Assign x = mdp.utils.rrep(...)

```python
x = mdp.utils.rrep(x, INDIM)
```

### Step 4: Assign unknown = value

```python
x[:, -1] = 2.0 * x[:, 0]
```

### Step 5: Assign y = mult(...)

```python
y = mult(x, beta)
```

### Step 6: Call py.test.raises()

```python
py.test.raises(mdp.NodeException, train_LRNode, [x], [y], False)
```


## Complete Example

```python
# Workflow
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
x = numx.linspace(-20, 20, TLEN)
x = mdp.utils.rrep(x, INDIM)
x[:, -1] = 2.0 * x[:, 0]
y = mult(x, beta)
py.test.raises(mdp.NodeException, train_LRNode, [x], [y], False)
```

## Next Steps


---

*Source: test_LinearRegressionNode.py:54 | Complexity: Intermediate | Last updated: 2026-05-18*