# How To: Pcanode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Parallel PCANode

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test Parallel PCANode'

```python
'Test Parallel PCANode'
```

**Verification:**
```python
assert_array_almost_equal(pca_node._cov_mtx._cov_mtx, parallel_pca_node._cov_mtx._cov_mtx, precision)
```

### Step 2: Assign precision = 6

```python
precision = 6
```

**Verification:**
```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

### Step 3: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([100, 10])
```

### Step 4: Assign x_test = numx_rand.random(...)

```python
x_test = numx_rand.random([20, 10])
```

### Step 5: Assign pca_node = mdp.nodes.PCANode(...)

```python
pca_node = mdp.nodes.PCANode()
```

### Step 6: Assign parallel_pca_node = parallel.ParallelPCANode(...)

```python
parallel_pca_node = parallel.ParallelPCANode()
```

### Step 7: Assign chunksize = 25

```python
chunksize = 25
```

### Step 8: Assign chunks = value

```python
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pca_node._cov_mtx._cov_mtx, parallel_pca_node._cov_mtx._cov_mtx, precision)
```

### Step 10: Call pca_node.stop_training()

```python
pca_node.stop_training()
```

### Step 11: Assign y1 = pca_node.execute(...)

```python
y1 = pca_node.execute(x_test)
```

### Step 12: Call parallel_pca_node.stop_training()

```python
parallel_pca_node.stop_training()
```

### Step 13: Assign y2 = parallel_pca_node.execute(...)

```python
y2 = parallel_pca_node.execute(x_test)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

### Step 15: Call pca_node.train()

```python
pca_node.train(chunk)
```

### Step 16: Assign forked_node = parallel_pca_node.fork(...)

```python
forked_node = parallel_pca_node.fork()
```

### Step 17: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 18: Call parallel_pca_node.join()

```python
parallel_pca_node.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test Parallel PCANode'
precision = 6
x = numx_rand.random([100, 10])
x_test = numx_rand.random([20, 10])
x *= numx.arange(1, 11)
x_test *= numx.arange(1, 11)
pca_node = mdp.nodes.PCANode()
parallel_pca_node = parallel.ParallelPCANode()
chunksize = 25
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
for chunk in chunks:
    pca_node.train(chunk)
    forked_node = parallel_pca_node.fork()
    forked_node.train(chunk)
    parallel_pca_node.join(forked_node)
assert_array_almost_equal(pca_node._cov_mtx._cov_mtx, parallel_pca_node._cov_mtx._cov_mtx, precision)
pca_node.stop_training()
y1 = pca_node.execute(x_test)
parallel_pca_node.stop_training()
y2 = parallel_pca_node.execute(x_test)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## Next Steps


---

*Source: test_parallelnodes.py:4 | Complexity: Advanced | Last updated: 2026-05-18*