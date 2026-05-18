# How To: Is Last Sets Completed To Total

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test is last sets completed to total

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `pytest`
- `pymc`
- `pymc.progress_bar`
- `pymc.progress_bar.marimo_progress`


## Step-by-Step Guide

### Step 1: Assign backend = MarimoProgressBackend(...)

```python
backend = MarimoProgressBackend(step_name='Draws', n_bars=2, total=150, combined=False, full_stats=False)
```

**Verification:**
```python
assert backend._task_state[0]['completed'] == 150
```

### Step 2: Call backend._initialize_tasks()

```python
backend._initialize_tasks()
```

**Verification:**
```python
assert backend._task_state[1]['completed'] == 0
```

### Step 3: Call backend.update()

```python
backend.update(task_id=0, advance=1, failing=False, stats={}, is_last=True)
```

**Verification:**
```python
assert backend._task_state[0]['completed'] == 150
```

### Step 4: Call backend.update()

```python
backend.update(task_id=0, advance=1, failing=False, stats={}, is_last=False)
```


## Complete Example

```python
# Workflow
backend = MarimoProgressBackend(step_name='Draws', n_bars=2, total=150, combined=False, full_stats=False)
backend._initialize_tasks()
for _ in range(150):
    backend.update(task_id=0, advance=1, failing=False, stats={}, is_last=False)
backend.update(task_id=0, advance=1, failing=False, stats={}, is_last=True)
assert backend._task_state[0]['completed'] == 150
assert backend._task_state[1]['completed'] == 0
```

## Next Steps


---

*Source: test_marimo.py:111 | Complexity: Intermediate | Last updated: 2026-05-18*