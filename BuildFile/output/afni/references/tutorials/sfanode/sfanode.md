# How To: Sfanode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Parallel SFANode

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test Parallel SFANode'

```python
'Test Parallel SFANode'
```

**Verification:**
```python
assert_array_almost_equal(sfa_node._cov_mtx._cov_mtx, parallel_sfa_node._cov_mtx._cov_mtx, precision)
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

### Step 5: Assign sfa_node = mdp.nodes.SFANode(...)

```python
sfa_node = mdp.nodes.SFANode()
```

### Step 6: Assign parallel_sfa_node = parallel.ParallelSFANode(...)

```python
parallel_sfa_node = parallel.ParallelSFANode()
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
assert_array_almost_equal(sfa_node._cov_mtx._cov_mtx, parallel_sfa_node._cov_mtx._cov_mtx, precision)
```

### Step 10: Call sfa_node.stop_training()

```python
sfa_node.stop_training()
```

### Step 11: Assign y1 = sfa_node.execute(...)

```python
y1 = sfa_node.execute(x_test)
```

### Step 12: Call parallel_sfa_node.stop_training()

```python
parallel_sfa_node.stop_training()
```

### Step 13: Assign y2 = parallel_sfa_node.execute(...)

```python
y2 = parallel_sfa_node.execute(x_test)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

### Step 15: Call sfa_node.train()

```python
sfa_node.train(chunk)
```

### Step 16: Assign forked_node = parallel_sfa_node.fork(...)

```python
forked_node = parallel_sfa_node.fork()
```

### Step 17: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 18: Call parallel_sfa_node.join()

```python
parallel_sfa_node.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test Parallel SFANode'
precision = 6
x = numx_rand.random([100, 10])
x_test = numx_rand.random([20, 10])
x *= numx.arange(1, 11)
x_test *= numx.arange(1, 11)
sfa_node = mdp.nodes.SFANode()
parallel_sfa_node = parallel.ParallelSFANode()
chunksize = 25
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
for chunk in chunks:
    sfa_node.train(chunk)
    forked_node = parallel_sfa_node.fork()
    forked_node.train(chunk)
    parallel_sfa_node.join(forked_node)
assert_array_almost_equal(sfa_node._cov_mtx._cov_mtx, parallel_sfa_node._cov_mtx._cov_mtx, precision)
sfa_node.stop_training()
y1 = sfa_node.execute(x_test)
parallel_sfa_node.stop_training()
y2 = parallel_sfa_node.execute(x_test)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## Next Steps


---

*Source: test_parallelnodes.py:31 | Complexity: Advanced | Last updated: 2026-05-18*