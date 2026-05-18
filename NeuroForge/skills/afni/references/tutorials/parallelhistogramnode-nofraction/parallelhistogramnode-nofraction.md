# How To: Parallelhistogramnode Nofraction

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test HistogramNode with fraction set to 1.0.

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test HistogramNode with fraction set to 1.0.'

```python
'Test HistogramNode with fraction set to 1.0.'
```

**Verification:**
```python
assert numx.all(x == node.data_hist)
```

### Step 2: Assign node = parallel.ParallelHistogramNode(...)

```python
node = parallel.ParallelHistogramNode()
```

### Step 3: Assign x1 = numx.array(...)

```python
x1 = numx.array([[0.1, 0.2], [0.3, 0.5]])
```

### Step 4: Assign x2 = numx.array(...)

```python
x2 = numx.array([[0.3, 0.6], [0.2, 0.1]])
```

### Step 5: Assign x = numx.concatenate(...)

```python
x = numx.concatenate([x1, x2])
```

### Step 6: Assign chunks = value

```python
chunks = [x1, x2]
```

**Verification:**
```python
assert numx.all(x == node.data_hist)
```

### Step 7: Call node.stop_training()

```python
node.stop_training()
```

### Step 8: Assign forked_node = node.fork(...)

```python
forked_node = node.fork()
```

### Step 9: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 10: Call node.join()

```python
node.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test HistogramNode with fraction set to 1.0.'
node = parallel.ParallelHistogramNode()
x1 = numx.array([[0.1, 0.2], [0.3, 0.5]])
x2 = numx.array([[0.3, 0.6], [0.2, 0.1]])
x = numx.concatenate([x1, x2])
chunks = [x1, x2]
for chunk in chunks:
    forked_node = node.fork()
    forked_node.train(chunk)
    node.join(forked_node)
assert numx.all(x == node.data_hist)
node.stop_training()
```

## Next Steps


---

*Source: test_parallelnodes.py:97 | Complexity: Advanced | Last updated: 2026-05-18*