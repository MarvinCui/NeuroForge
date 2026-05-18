# How To: Process Scheduler Shutdown

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can properly shutdown the subprocesses

## Prerequisites

**Required Modules:**
- `__future__`
- `_tools`
- `mdp.parallel`


## Step-by-Step Guide

### Step 1: 'Test that we can properly shutdown the subprocesses'

```python
'Test that we can properly shutdown the subprocesses'
```

### Step 2: Assign scheduler = parallel.ProcessScheduler(...)

```python
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=1, source_paths=None, cache_callable=False)
```

### Step 3: Call scheduler.shutdown()

```python
scheduler.shutdown()
```


## Complete Example

```python
# Workflow
'Test that we can properly shutdown the subprocesses'
scheduler = parallel.ProcessScheduler(verbose=False, n_processes=1, source_paths=None, cache_callable=False)
scheduler.shutdown()
```

## Next Steps


---

*Source: test_process_schedule.py:7 | Complexity: Beginner | Last updated: 2026-05-18*