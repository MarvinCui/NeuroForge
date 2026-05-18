# How To: Layer Invertibility

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Layer invertibility

## Prerequisites

**Required Modules:**
- `__future__`
- `py.test`
- `StringIO`
- `mdp.hinet`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign layer = mh.Layer(...)

```python
layer = mh.Layer(_pca_nodes([10, 17, 3], [10, 17, 3]))
```

**Verification:**
```python
assert numx.all(numx.absolute(x - x_inverse) < 0.001)
```

### Step 2: Assign x = numx_rand.random.astype(...)

```python
x = numx_rand.random([100, 30]).astype('f')
```

### Step 3: Call layer.train()

```python
layer.train(x)
```

### Step 4: Assign y = layer.execute(...)

```python
y = layer.execute(x)
```

### Step 5: Assign x_inverse = layer.inverse(...)

```python
x_inverse = layer.inverse(y)
```

**Verification:**
```python
assert numx.all(numx.absolute(x - x_inverse) < 0.001)
```


## Complete Example

```python
# Workflow
layer = mh.Layer(_pca_nodes([10, 17, 3], [10, 17, 3]))
x = numx_rand.random([100, 30]).astype('f')
layer.train(x)
y = layer.execute(x)
x_inverse = layer.inverse(y)
assert numx.all(numx.absolute(x - x_inverse) < 0.001)
```

## Next Steps


---

*Source: test_hinet.py:152 | Complexity: Intermediate | Last updated: 2026-05-18*