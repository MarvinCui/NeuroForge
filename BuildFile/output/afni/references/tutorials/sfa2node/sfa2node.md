# How To: Sfa2Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Parallel SFA2Node

## Prerequisites

**Required Modules:**
- `mdp.parallel`
- `_tools`


## Step-by-Step Guide

### Step 1: 'Test Parallel SFA2Node'

```python
'Test Parallel SFA2Node'
```

### Step 2: Assign x = numx_rand.random(...)

```python
x = numx_rand.random([100, 10])
```

### Step 3: Assign x_test = numx_rand.random(...)

```python
x_test = numx_rand.random([20, 10])
```

### Step 4: Assign node = mdp.nodes.SFA2Node(...)

```python
node = mdp.nodes.SFA2Node()
```

### Step 5: Assign chunksize = 25

```python
chunksize = 25
```

### Step 6: Assign chunks = value

```python
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
```

### Step 7: Call node.stop_training()

```python
node.stop_training()
```

### Step 8: Call node.execute()

```python
node.execute(x_test)
```

### Step 9: Assign forked_node = node.fork(...)

```python
forked_node = node.fork()
```

### Step 10: Call forked_node.train()

```python
forked_node.train(chunk)
```

### Step 11: Call node.join()

```python
node.join(forked_node)
```


## Complete Example

```python
# Workflow
'Test Parallel SFA2Node'
x = numx_rand.random([100, 10])
x_test = numx_rand.random([20, 10])
x *= numx.arange(1, 11)
x_test *= numx.arange(1, 11)
node = mdp.nodes.SFA2Node()
chunksize = 25
chunks = [x[i * chunksize:(i + 1) * chunksize] for i in xrange(len(x) // chunksize)]
for chunk in chunks:
    forked_node = node.fork()
    forked_node.train(chunk)
    node.join(forked_node)
node.stop_training()
node.execute(x_test)
```

## Next Steps


---

*Source: test_parallelnodes.py:156 | Complexity: Advanced | Last updated: 2026-05-18*