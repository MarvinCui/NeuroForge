# How To: Linearregressionnode Raises On Wrong Output Size

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LinearRegressionNode raises on wrong output size

## Prerequisites

**Required Modules:**
- `py.test`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign beta = numx_rand.uniform(...)

```python
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
```

### Step 2: Assign x = numx_rand.uniform(...)

```python
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
```

### Step 3: Assign unknown = value

```python
x[:, -1] = 2.0 * x[:, 0]
```

### Step 4: Assign y = mult(...)

```python
y = mult(x, beta)
```

### Step 5: Assign y = value

```python
y = y[:10, :]
```

### Step 6: Call py.test.raises()

```python
py.test.raises(mdp.TrainingException, train_LRNode, [x], [y], False)
```


## Complete Example

```python
# Workflow
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
x[:, -1] = 2.0 * x[:, 0]
y = mult(x, beta)
y = y[:10, :]
py.test.raises(mdp.TrainingException, train_LRNode, [x], [y], False)
```

## Next Steps


---

*Source: test_LinearRegressionNode.py:63 | Complexity: Intermediate | Last updated: 2026-05-18*