# How To: Process Scheduler Order

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the correct result order in process scheduler.

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test the correct result order in process scheduler.'

```python
'Test the correct result order in process scheduler.'
```

**Verification:**
```python
assert n.all(results == n.concatenate([n.arange(0, i + 1) ** 2 for i in xrange(max_i)]))
```

### Step 2: Assign scheduler = parallel.ProcessScheduler(...)

```python
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=3, source_paths=None)
```

### Step 3: Assign max_i = 8

```python
max_i = 8
```

### Step 4: Assign results = scheduler.get_results(...)

```python
results = scheduler.get_results()
```

### Step 5: Call scheduler.shutdown()

```python
scheduler.shutdown()
```

### Step 6: Assign results = n.concatenate(...)

```python
results = n.concatenate(results)
```

**Verification:**
```python
assert n.all(results == n.concatenate([n.arange(0, i + 1) ** 2 for i in xrange(max_i)]))
```

### Step 7: Call scheduler.add_task()

```python
scheduler.add_task((n.arange(0, i + 1), (max_i - 1 - i) * 1.0 / 4), parallel.SleepSqrTestCallable())
```


## Complete Example

```python
# Workflow
'Test the correct result order in process scheduler.'
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=3, source_paths=None)
max_i = 8
for i in xrange(max_i):
    scheduler.add_task((n.arange(0, i + 1), (max_i - 1 - i) * 1.0 / 4), parallel.SleepSqrTestCallable())
results = scheduler.get_results()
scheduler.shutdown()
results = n.concatenate(results)
assert n.all(results == n.concatenate([n.arange(0, i + 1) ** 2 for i in xrange(max_i)]))
```

## Next Steps


---

*Source: test_process_schedule.py:15 | Complexity: Intermediate | Last updated: 2026-05-18*