# How To: Process Scheduler Flow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test process scheduler with real Nodes.

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test process scheduler with real Nodes.'

```python
'Test process scheduler with real Nodes.'
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

### Step 8: Assign input_dim = 30

```python
input_dim = 30
```

### Step 9: Assign scales = n.linspace(...)

```python
scales = n.linspace(1, 100, num=input_dim)
```

### Step 10: Assign scale_matrix = mdp.numx.diag(...)

```python
scale_matrix = mdp.numx.diag(scales)
```

### Step 11: Assign train_iterables = value

```python
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
```

### Step 12: Assign x = mdp.numx.random.random(...)

```python
x = mdp.numx.random.random((10, input_dim))
```

### Step 13: Call flow.train()

```python
flow.train(train_iterables)
```

**Verification:**
```python
assert parallel_flow[0].tlen == flow[0].tlen
```

### Step 14: Assign y1 = flow.execute(...)

```python
y1 = flow.execute(x)
```

### Step 15: Assign y2 = parallel_flow.execute(...)

```python
y2 = parallel_flow.execute(x)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

### Step 17: Call parallel_flow.train()

```python
parallel_flow.train(train_iterables, scheduler=scheduler)
```

### Step 18: Call parallel_flow.execute()

```python
parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
```


## Complete Example

```python
# Workflow
'Test process scheduler with real Nodes.'
precision = 6
node1 = mdp.nodes.PCANode(output_dim=20)
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
node3 = mdp.nodes.SFANode(output_dim=10)
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
input_dim = 30
scales = n.linspace(1, 100, num=input_dim)
scale_matrix = mdp.numx.diag(scales)
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
x = mdp.numx.random.random((10, input_dim))
with parallel.ProcessScheduler(verbose=False, n_processes=3, source_paths=None) as scheduler:
    parallel_flow.train(train_iterables, scheduler=scheduler)
    parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
flow.train(train_iterables)
assert parallel_flow[0].tlen == flow[0].tlen
y1 = flow.execute(x)
y2 = parallel_flow.execute(x)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## Next Steps


---

*Source: test_process_schedule.py:57 | Complexity: Advanced | Last updated: 2026-05-18*