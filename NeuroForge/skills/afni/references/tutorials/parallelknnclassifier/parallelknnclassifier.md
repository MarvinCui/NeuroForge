# How To: Parallelknnclassifier

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ParallelGaussianClassifier.

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test ParallelGaussianClassifier.'

```python
'Test ParallelGaussianClassifier.'
```

**Verification:**
```python
assert_array_almost_equal(node.samples, pnode.samples, precision)
```

### Step 2: Assign precision = 6

```python
precision = 6
```

**Verification:**
```python
assert node.n_samples == pnode.n_samples
```

### Step 3: Assign xs = value

```python
xs = [numx_rand.random([3, 2]) for _ in range(8)]
```

### Step 4: Assign labels = value

```python
labels = [1, 2, 1, 1, 2, 3, 2, 3]
```

### Step 5: Assign node = mdp.nodes.KNNClassifier(...)

```python
node = mdp.nodes.KNNClassifier()
```

### Step 6: Assign pnode = parallel.ParallelKNNClassifier(...)

```python
pnode = parallel.ParallelKNNClassifier()
```

### Step 7: Call node.stop_training()

```python
node.stop_training()
```

### Step 8: Assign pnode1 = pnode.fork(...)

```python
pnode1 = pnode.fork()
```

### Step 9: Assign pnode2 = pnode.fork(...)

```python
pnode2 = pnode.fork()
```

### Step 10: Call pnode.join()

```python
pnode.join(pnode1)
```

### Step 11: Call pnode.join()

```python
pnode.join(pnode2)
```

### Step 12: Call pnode.stop_training()

```python
pnode.stop_training()
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(node.samples, pnode.samples, precision)
```

**Verification:**
```python
assert node.n_samples == pnode.n_samples
```

### Step 14: Call node.train()

```python
node.train(x, labels[i])
```

### Step 15: Call pnode1.train()

```python
pnode1.train(x, labels[i])
```

### Step 16: Call pnode2.train()

```python
pnode2.train(x, labels[i])
```


## Complete Example

```python
# Workflow
'Test ParallelGaussianClassifier.'
precision = 6
xs = [numx_rand.random([3, 2]) for _ in range(8)]
labels = [1, 2, 1, 1, 2, 3, 2, 3]
node = mdp.nodes.KNNClassifier()
pnode = parallel.ParallelKNNClassifier()
for i, x in enumerate(xs):
    node.train(x, labels[i])
node.stop_training()
pnode1 = pnode.fork()
pnode2 = pnode.fork()
for i, x in enumerate(xs):
    if i < 4:
        pnode1.train(x, labels[i])
    else:
        pnode2.train(x, labels[i])
pnode.join(pnode1)
pnode.join(pnode2)
pnode.stop_training()
assert_array_almost_equal(node.samples, pnode.samples, precision)
assert node.n_samples == pnode.n_samples
```

## Next Steps


---

*Source: test_parallelclassifiers.py:64 | Complexity: Advanced | Last updated: 2026-05-18*