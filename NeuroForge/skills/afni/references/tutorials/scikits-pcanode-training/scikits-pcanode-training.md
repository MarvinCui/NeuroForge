# How To: Scikits Pcanode Training

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check functionality of scikits' PCANode.

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: "Check functionality of scikits' PCANode."

```python
"Check functionality of scikits' PCANode."
```

**Verification:**
```python
assert y.shape[1] == 2
```

### Step 2: Assign node = mdp.nodes.PCAScikitsLearnNode(...)

```python
node = mdp.nodes.PCAScikitsLearnNode(n_components=2)
```

**Verification:**
```python
assert y.shape[0] == T
```

### Step 3: Assign T = 50000

```python
T = 50000
```

**Verification:**
```python
assert_array_almost_equal(y[:, 0] / 100.0, x[:, 3] / 100.0, 1)
```

### Step 4: Assign x = numx_rand.randn(...)

```python
x = numx_rand.randn(T, 4)
```

**Verification:**
```python
assert_array_almost_equal(y[:, 1] / 10.0, x[:, 1] / 10.0, 1)
```

### Step 5: Call node.train()

```python
node.train(x)
```

### Step 6: Call node.stop_training()

```python
node.stop_training()
```

### Step 7: Assign y = node.execute(...)

```python
y = node.execute(x)
```

**Verification:**
```python
assert y.shape[1] == 2
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(y[:, 0] / 100.0, x[:, 3] / 100.0, 1)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(y[:, 1] / 10.0, x[:, 1] / 10.0, 1)
```


## Complete Example

```python
# Workflow
"Check functionality of scikits' PCANode."
node = mdp.nodes.PCAScikitsLearnNode(n_components=2)
T = 50000
x = numx_rand.randn(T, 4)
x[:, 1] *= 10.0
x[:, 3] *= 100.0
node.train(x)
node.stop_training()
y = node.execute(x)
assert y.shape[1] == 2
assert y.shape[0] == T
if (y[:, 0] * x[:, 3]).mean() < 0.0:
    y[:, 0] *= -1.0
if (y[:, 1] * x[:, 1]).mean() < 0.0:
    y[:, 1] *= -1.0
assert_array_almost_equal(y[:, 0] / 100.0, x[:, 3] / 100.0, 1)
assert_array_almost_equal(y[:, 1] / 10.0, x[:, 1] / 10.0, 1)
```

## Next Steps


---

*Source: test_scikits.py:13 | Complexity: Advanced | Last updated: 2026-05-18*