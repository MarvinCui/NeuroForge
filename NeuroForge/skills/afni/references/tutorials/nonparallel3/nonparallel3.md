# How To: Nonparallel3

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test training for non-parallel nodes.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test training for non-parallel nodes.'

```python
'Test training for non-parallel nodes.'
```

### Step 2: Assign sfa_node = mdp.nodes.SFANode(...)

```python
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
```

### Step 3: Assign sfa2_node = mdp.nodes.SFA2Node(...)

```python
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
```

### Step 4: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([sfa_node, sfa2_node])
```

### Step 5: Assign data_iterables = value

```python
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
```

### Step 6: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 7: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```

### Step 8: Assign x = n.random.random(...)

```python
x = n.random.random([100, 10])
```

### Step 9: Call flow.execute()

```python
flow.execute(x)
```

### Step 10: Assign results = value

```python
results = []
```

### Step 11: Call flow.use_results()

```python
flow.use_results(results)
```

### Step 12: Assign task = flow.get_task(...)

```python
task = flow.get_task()
```

### Step 13: Call results.append()

```python
results.append(task())
```


## Complete Example

```python
# Workflow
'Test training for non-parallel nodes.'
sfa_node = mdp.nodes.SFANode(input_dim=10, output_dim=8)
sfa2_node = mdp.nodes.SFA2Node(input_dim=8, output_dim=6)
flow = parallel.ParallelFlow([sfa_node, sfa2_node])
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
while flow.is_parallel_training:
    results = []
    while flow.task_available():
        task = flow.get_task()
        results.append(task())
    flow.use_results(results)
x = n.random.random([100, 10])
flow.execute(x)
```

## Next Steps


---

*Source: test_parallelflows.py:169 | Complexity: Advanced | Last updated: 2026-05-18*