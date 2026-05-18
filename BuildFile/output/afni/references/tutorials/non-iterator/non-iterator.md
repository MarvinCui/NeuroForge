# How To: Non Iterator

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test parallel training and execution with a single array.

## Prerequisites

**Required Modules:**
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test parallel training and execution with a single array.'

```python
'Test parallel training and execution with a single array.'
```

### Step 2: Assign flow = parallel.ParallelFlow(...)

```python
flow = parallel.ParallelFlow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=3), mdp.nodes.SFANode(output_dim=20)])
```

### Step 3: Assign data_iterables = value

```python
data_iterables = n.random.random((200, 10)) * n.arange(1, 11)
```

### Step 4: Assign scheduler = parallel.Scheduler(...)

```python
scheduler = parallel.Scheduler()
```

### Step 5: Call flow.train()

```python
flow.train(data_iterables, scheduler=scheduler)
```

### Step 6: Assign x = n.random.random(...)

```python
x = n.random.random((100, 10))
```

### Step 7: Call flow.execute()

```python
flow.execute(x)
```


## Complete Example

```python
# Workflow
'Test parallel training and execution with a single array.'
flow = parallel.ParallelFlow([mdp.nodes.SFANode(output_dim=5), mdp.nodes.PolynomialExpansionNode(degree=3), mdp.nodes.SFANode(output_dim=20)])
data_iterables = n.random.random((200, 10)) * n.arange(1, 11)
scheduler = parallel.Scheduler()
flow.train(data_iterables, scheduler=scheduler)
x = n.random.random((100, 10))
flow.execute(x)
```

## Next Steps


---

*Source: test_parallelflows.py:23 | Complexity: Intermediate | Last updated: 2026-05-18*