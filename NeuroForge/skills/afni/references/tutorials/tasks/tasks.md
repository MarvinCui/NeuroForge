# How To: Tasks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parallel training and execution by running the tasks.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test parallel training and execution by running the tasks.'

```python
'Test parallel training and execution by running the tasks.'
```

### Step 2: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=3), mdp.nodes.SFANode(output_dim=20)])
```

### Step 3: Assign data_iterables = value

```python
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], None, [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
```

### Step 4: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 5: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```

### Step 6: Assign iterable = value

```python
iterable = [n.random.random((20, 10)) for _ in xrange(6)]
```

### Step 7: Call flow.execute()

```python
flow.execute(iterable, scheduler=scheduler)
```


## Complete Example

```python
# Workflow
'Test parallel training and execution by running the tasks.'
flow = parallel.ParallelFlow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=3), mdp.nodes.SFANode(output_dim=20)])
data_iterables = [[n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)], None, [n.random.random((30, 10)) * n.arange(1, 11) for _ in xrange(6)]]
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
iterable = [n.random.random((20, 10)) for _ in xrange(6)]
flow.execute(iterable, scheduler=scheduler)
```

## Next Steps


---

*Source: test_parallelflows.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*