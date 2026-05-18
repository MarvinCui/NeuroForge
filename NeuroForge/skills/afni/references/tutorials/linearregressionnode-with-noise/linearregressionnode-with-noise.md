# How To: Linearregressionnode With Noise

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LinearRegressionNode with noise

## Prerequisites

**Required Modules:**
- `py.test`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign beta = numx_rand.uniform(...)

```python
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM + 1, OUTDIM))
```

**Verification:**
```python
assert_array_almost_equal(lrnode.beta, beta, 2)
```

### Step 2: Assign x = numx_rand.uniform(...)

```python
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
```

**Verification:**
```python
assert_array_almost_equal_diff(res, out[0], 2)
```

### Step 3: Assign y = value

```python
y = mult(x, beta[1:, :]) + beta[0, :]
```

### Step 4: Assign inp = value

```python
inp = [numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM)) for i in xrange(5)]
```

### Step 5: Assign out = value

```python
out = [mult(x, beta[1:, :]) + beta[0, :] + numx_rand.normal(size=y.shape) * 0.1 for x in inp]
```

### Step 6: Assign lrnode = train_LRNode(...)

```python
lrnode = train_LRNode(inp, out, True)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(lrnode.beta, beta, 2)
```

### Step 8: Assign res = lrnode(...)

```python
res = lrnode(inp[0])
```

### Step 9: Call assert_array_almost_equal_diff()

```python
assert_array_almost_equal_diff(res, out[0], 2)
```


## Complete Example

```python
# Workflow
beta = numx_rand.uniform(-10.0, 10.0, size=(INDIM + 1, OUTDIM))
x = numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM))
y = mult(x, beta[1:, :]) + beta[0, :]
inp = [numx_rand.uniform(-20.0, 20.0, size=(TLEN, INDIM)) for i in xrange(5)]
out = [mult(x, beta[1:, :]) + beta[0, :] + numx_rand.normal(size=y.shape) * 0.1 for x in inp]
lrnode = train_LRNode(inp, out, True)
assert_array_almost_equal(lrnode.beta, beta, 2)
res = lrnode(inp[0])
assert_array_almost_equal_diff(res, out[0], 2)
```

## Next Steps


---

*Source: test_LinearRegressionNode.py:39 | Complexity: Advanced | Last updated: 2026-05-18*