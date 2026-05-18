# How To: Process Scheduler No Cache

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test process scheduler with caching turned off.

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test process scheduler with caching turned off.'

```python
'Test process scheduler with caching turned off.'
```

**Verification:**
```python
assert n.all(results == n.array([0, 1, 4, 9, 16, 25, 36, 49]))
```

### Step 2: Assign scheduler = parallel.ProcessScheduler(...)

```python
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=2, source_paths=None, cache_callable=False)
```

### Step 3: Assign results = scheduler.get_results(...)

```python
results = scheduler.get_results()
```

### Step 4: Call scheduler.shutdown()

```python
scheduler.shutdown()
```

### Step 5: Assign results = n.array(...)

```python
results = n.array(results)
```

**Verification:**
```python
assert n.all(results == n.array([0, 1, 4, 9, 16, 25, 36, 49]))
```

### Step 6: Call scheduler.add_task()

```python
scheduler.add_task(i, parallel.SqrTestCallable())
```


## Complete Example

```python
# Workflow
'Test process scheduler with caching turned off.'
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=2, source_paths=None, cache_callable=False)
for i in xrange(8):
    scheduler.add_task(i, parallel.SqrTestCallable())
results = scheduler.get_results()
scheduler.shutdown()
results = n.array(results)
assert n.all(results == n.array([0, 1, 4, 9, 16, 25, 36, 49]))
```

## Next Steps


---

*Source: test_process_schedule.py:32 | Complexity: Intermediate | Last updated: 2026-05-18*