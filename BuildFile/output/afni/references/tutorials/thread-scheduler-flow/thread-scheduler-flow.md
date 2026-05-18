# How To: Thread Scheduler Flow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test thread scheduler with real Nodes.

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test thread scheduler with real Nodes.'

```python
'Test thread scheduler with real Nodes.'
```

**Verification:**
```python
assert parallel_flow[0].tlen == flow[0].tlen
```

### Step 2: Assign precision = 6

```python
precision = 6
```

**Verification:**
```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

### Step 3: Assign node1 = mdp.nodes.PCANode(...)

```python
node1 = mdp.nodes.PCANode(output_dim=20)
```

### Step 4: Assign node2 = mdp.nodes.PolynomialExpansionNode(...)

```python
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
```

### Step 5: Assign node3 = mdp.nodes.SFANode(...)

```python
node3 = mdp.nodes.SFANode(output_dim=10)
```

### Step 6: Assign flow = mdp.parallel.ParallelFlow(...)

```python
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
```

### Step 7: Assign parallel_flow = mdp.parallel.ParallelFlow(...)

```python
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
```

### Step 8: Assign scheduler = parallel.ThreadScheduler(...)

```python
scheduler = parallel.ThreadScheduler(verbose=False, n_threads=3)
```

### Step 9: Assign input_dim = 30

```python
input_dim = 30
```

### Step 10: Assign scales = n.linspace(...)

```python
scales = n.linspace(1, 100, num=input_dim)
```

### Step 11: Assign scale_matrix = mdp.numx.diag(...)

```python
scale_matrix = mdp.numx.diag(scales)
```

### Step 12: Assign train_iterables = value

```python
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
```

### Step 13: Call parallel_flow.train()

```python
parallel_flow.train(train_iterables, scheduler=scheduler)
```

### Step 14: Assign x = mdp.numx.random.random(...)

```python
x = mdp.numx.random.random((10, input_dim))
```

### Step 15: Call parallel_flow.execute()

```python
parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
```

### Step 16: Call scheduler.shutdown()

```python
scheduler.shutdown()
```

### Step 17: Call flow.train()

```python
flow.train(train_iterables)
```

**Verification:**
```python
assert parallel_flow[0].tlen == flow[0].tlen
```

### Step 18: Assign y1 = flow.execute(...)

```python
y1 = flow.execute(x)
```

### Step 19: Assign y2 = parallel_flow.execute(...)

```python
y2 = parallel_flow.execute(x)
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```


## Complete Example

```python
# Workflow
'Test thread scheduler with real Nodes.'
precision = 6
node1 = mdp.nodes.PCANode(output_dim=20)
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
node3 = mdp.nodes.SFANode(output_dim=10)
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
scheduler = parallel.ThreadScheduler(verbose=False, n_threads=3)
input_dim = 30
scales = n.linspace(1, 100, num=input_dim)
scale_matrix = mdp.numx.diag(scales)
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
parallel_flow.train(train_iterables, scheduler=scheduler)
x = mdp.numx.random.random((10, input_dim))
parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
scheduler.shutdown()
flow.train(train_iterables)
assert parallel_flow[0].tlen == flow[0].tlen
y1 = flow.execute(x)
y2 = parallel_flow.execute(x)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## Next Steps


---

*Source: test_schedule.py:52 | Complexity: Advanced | Last updated: 2026-05-18*