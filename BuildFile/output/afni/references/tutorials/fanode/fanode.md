# How To: Fanode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FANode

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign d = 10

```python
d = 10
```

**Verification:**
```python
assert_array_almost_equal(fa.mu[0, :], mean(x, axis=0), 5)
```

### Step 2: Assign N = 5000

```python
N = 5000
```

**Verification:**
```python
assert_array_almost_equal(fa.sigma, std(noise, axis=0) ** 2, 2)
```

### Step 3: Assign k = 4

```python
k = 4
```

**Verification:**
```python
assert sum(s / max(s) > 0.01) == k, 'A and its estimation do not span the same subspace'
```

### Step 4: Assign mu = value

```python
mu = uniform((1, d)) * 3.0 + 2.0
```

**Verification:**
```python
assert_array_almost_equal(numx.diag(numx.cov(est, rowvar=0)), fa.sigma, 3)
```

### Step 5: Assign sigma = value

```python
sigma = uniform((d,)) * 0.01
```

**Verification:**
```python
assert_almost_equal(numx.amax(abs(numx.mean(est, axis=0)), axis=None), 0.0, 3)
```

### Step 6: Assign A = numx_rand.normal(...)

```python
A = numx_rand.normal(size=(k, d))
```

**Verification:**
```python
assert_array_almost_equal_diff(numx.cov(est, rowvar=0), mdp.utils.mult(fa.A, fa.A.T), 1)
```

### Step 7: Assign y = numx_rand.normal(...)

```python
y = numx_rand.normal(0.0, 1.0, size=(N, k))
```

### Step 8: Assign noise = value

```python
noise = numx_rand.normal(0.0, 1.0, size=(N, d)) * sigma
```

### Step 9: Assign x = value

```python
x = mult(y, A) + mu + noise
```

### Step 10: Assign fa = mdp.nodes.FANode(...)

```python
fa = mdp.nodes.FANode(output_dim=k, dtype='d')
```

### Step 11: Call fa.train()

```python
fa.train(x)
```

### Step 12: Call fa.stop_training()

```python
fa.stop_training()
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fa.mu[0, :], mean(x, axis=0), 5)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fa.sigma, std(noise, axis=0) ** 2, 2)
```

### Step 15: Assign AA = numx.concatenate(...)

```python
AA = numx.concatenate((A, fa.A.T), axis=0)
```

### Step 16: Assign unknown = utils.svd(...)

```python
u, s, vh = utils.svd(AA)
```

**Verification:**
```python
assert sum(s / max(s) > 0.01) == k, 'A and its estimation do not span the same subspace'
```

### Step 17: Assign y = fa.execute(...)

```python
y = fa.execute(x)
```

### Step 18: Call fa.generate_input()

```python
fa.generate_input()
```

### Step 19: Call fa.generate_input()

```python
fa.generate_input(10)
```

### Step 20: Call fa.generate_input()

```python
fa.generate_input(y)
```

### Step 21: Call fa.generate_input()

```python
fa.generate_input(y, noise=True)
```

### Step 22: Assign est = fa.generate_input(...)

```python
est = fa.generate_input(numx.zeros((N, k)), noise=True)
```

### Step 23: Call assert_array_almost_equal()

```python
assert_array_almost_equal(numx.diag(numx.cov(est, rowvar=0)), fa.sigma, 3)
```

### Step 24: Call assert_almost_equal()

```python
assert_almost_equal(numx.amax(abs(numx.mean(est, axis=0)), axis=None), 0.0, 3)
```

### Step 25: Assign est = fa.generate_input(...)

```python
est = fa.generate_input(100000)
```

### Step 26: Call assert_array_almost_equal_diff()

```python
assert_array_almost_equal_diff(numx.cov(est, rowvar=0), mdp.utils.mult(fa.A, fa.A.T), 1)
```


## Complete Example

```python
# Workflow
d = 10
N = 5000
k = 4
mu = uniform((1, d)) * 3.0 + 2.0
sigma = uniform((d,)) * 0.01
A = numx_rand.normal(size=(k, d))
y = numx_rand.normal(0.0, 1.0, size=(N, k))
noise = numx_rand.normal(0.0, 1.0, size=(N, d)) * sigma
x = mult(y, A) + mu + noise
fa = mdp.nodes.FANode(output_dim=k, dtype='d')
fa.train(x)
fa.stop_training()
assert_array_almost_equal(fa.mu[0, :], mean(x, axis=0), 5)
assert_array_almost_equal(fa.sigma, std(noise, axis=0) ** 2, 2)
AA = numx.concatenate((A, fa.A.T), axis=0)
u, s, vh = utils.svd(AA)
assert sum(s / max(s) > 0.01) == k, 'A and its estimation do not span the same subspace'
y = fa.execute(x)
fa.generate_input()
fa.generate_input(10)
fa.generate_input(y)
fa.generate_input(y, noise=True)
est = fa.generate_input(numx.zeros((N, k)), noise=True)
est -= fa.mu
assert_array_almost_equal(numx.diag(numx.cov(est, rowvar=0)), fa.sigma, 3)
assert_almost_equal(numx.amax(abs(numx.mean(est, axis=0)), axis=None), 0.0, 3)
est = fa.generate_input(100000)
assert_array_almost_equal_diff(numx.cov(est, rowvar=0), mdp.utils.mult(fa.A, fa.A.T), 1)
```

## Next Steps


---

*Source: test_FANode.py:3 | Complexity: Advanced | Last updated: 2026-05-18*