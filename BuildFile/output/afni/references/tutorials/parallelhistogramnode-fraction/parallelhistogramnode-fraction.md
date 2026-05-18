# How To: Parallelhistogramnode Fraction

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test HistogramNode with fraction set to 0.5.

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test HistogramNode with fraction set to 0.5.'

```python
'Test HistogramNode with fraction set to 0.5.'
```

**Verification:**
```python
assert len(node.data_hist) < 1000
```

### Step 2: Assign node = parallel.ParallelHistogramNode(...)

```python
node = parallel.ParallelHistogramNode(hist_fraction=0.5)
```

### Step 3: Assign x1 = numx.random.random(...)

```python
x1 = numx.random.random((1000, 3))
```

### Step 4: Assign x2 = numx.random.random(...)

```python
x2 = numx.random.random((500, 3))
```

### Step 5: Assign chunks = value

```python
chunks = [x1, x2]
```

**Verification:**
```python
assert len(node.data_hist) < 1000
```

### Step 6: Assign forked_node = node.fork(...)

```python
forked_node = node.fork()
```

### Step 7: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 8: Call node.join()

```python
node.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test HistogramNode with fraction set to 0.5.'
node = parallel.ParallelHistogramNode(hist_fraction=0.5)
x1 = numx.random.random((1000, 3))
x2 = numx.random.random((500, 3))
chunks = [x1, x2]
for chunk in chunks:
    forked_node = node.fork()
    forked_node.train(chunk)
    node.join(forked_node)
assert len(node.data_hist) < 1000
```

## Next Steps


---

*Source: test_parallelnodes.py:111 | Complexity: Advanced | Last updated: 2026-05-18*