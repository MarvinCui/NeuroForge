# How To: Linearregressionnode

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LinearRegressionNode

## Prerequisites

**Required Modules:**
- `py.test`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign beta = numx_rand.uniform(...)

```python
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
```

**Verification:**
```python
assert_array_almost_equal(lrnode.beta, beta, decimal)
```

### Step 2: Assign x = numx_rand.uniform(...)

```python
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
```

**Verification:**
```python
assert_array_almost_equal(res, y, decimal)
```

### Step 3: Assign y = mult(...)

```python
y = mult(x, beta)
```

### Step 4: Assign lrnode = train_LRNode(...)

```python
lrnode = train_LRNode([x], [y], False)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(lrnode.beta, beta, decimal)
```

### Step 6: Assign res = lrnode(...)

```python
res = lrnode(x)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res, y, decimal)
```


## Complete Example

```python
# Workflow
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM, OUTDIM))
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
y = mult(x, beta)
lrnode = train_LRNode([x], [y], False)
assert_array_almost_equal(lrnode.beta, beta, decimal)
res = lrnode(x)
assert_array_almost_equal(res, y, decimal)
```

## Next Steps


---

*Source: test_LinearRegressionNode.py:13 | Complexity: Intermediate | Last updated: 2026-05-18*