# How To: Process Scheduler Mdp Version

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we are running the same mdp in subprocesses

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test that we are running the same mdp in subprocesses'

```python
'Test that we are running the same mdp in subprocesses'
```

**Verification:**
```python
assert out[0] == out[1], 'Subprocesses did not run the same MDP as the parent:\n%s\n--\n%s' % (out[0], out[1])
```

### Step 2: Assign scheduler = parallel.ProcessScheduler(...)

```python
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=2, source_paths=None, cache_callable=False)
```

### Step 3: Assign out = scheduler.get_results(...)

```python
out = scheduler.get_results()
```

### Step 4: Call scheduler.shutdown()

```python
scheduler.shutdown()
```

**Verification:**
```python
assert out[0] == out[1], 'Subprocesses did not run the same MDP as the parent:\n%s\n--\n%s' % (out[0], out[1])
```

### Step 5: Call scheduler.add_task()

```python
scheduler.add_task(i, parallel.MDPVersionCallable())
```


## Complete Example

```python
# Workflow
'Test that we are running the same mdp in subprocesses'
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=2, source_paths=None, cache_callable=False)
for i in xrange(2):
    scheduler.add_task(i, parallel.MDPVersionCallable())
out = scheduler.get_results()
scheduler.shutdown()
assert out[0] == out[1], 'Subprocesses did not run the same MDP as the parent:\n%s\n--\n%s' % (out[0], out[1])
```

## Next Steps


---

*Source: test_process_schedule.py:86 | Complexity: Intermediate | Last updated: 2026-05-18*