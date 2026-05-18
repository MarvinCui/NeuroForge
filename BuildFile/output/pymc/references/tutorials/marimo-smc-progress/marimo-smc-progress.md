# How To: Marimo Smc Progress

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test marimo smc progress

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
backend = MarimoProgressBackend(step_name='Stage', n_bars=1, total=1.0, combined=False, full_stats=False)
```

**Verification:**
```python
assert backend._task_state[0]['total'] == 1.0
```

### Step 2: Call backend._initialize_tasks()

```python
backend._initialize_tasks()
```

**Verification:**
```python
assert backend._task_state[0]['completed'] == 0
```

### Step 3: Assign betas = value

```python
betas = [0.3, 0.7, 1.0]
```

**Verification:**
```python
assert backend._task_state[0]['completed'] == 1.0
```

### Step 4: Assign old = 0.0

```python
old = 0.0
```

**Verification:**
```python
assert backend._task_state[0]['completed'] == 1.0
```

### Step 5: Call backend.update()

```python
backend.update(task_id=0, advance=beta - old, failing=False, stats={}, is_last=beta >= 1.0)
```

### Step 6: Assign old = beta

```python
old = beta
```


## Complete Example

```python
# Workflow
backend = MarimoProgressBackend(step_name='Stage', n_bars=1, total=1.0, combined=False, full_stats=False)
backend._initialize_tasks()
assert backend._task_state[0]['total'] == 1.0
assert backend._task_state[0]['completed'] == 0
betas = [0.3, 0.7, 1.0]
old = 0.0
for beta in betas:
    backend.update(task_id=0, advance=beta - old, failing=False, stats={}, is_last=beta >= 1.0)
    old = beta
assert backend._task_state[0]['completed'] == 1.0
```

## Next Steps


---

*Source: test_marimo.py:124 | Complexity: Intermediate | Last updated: 2026-05-18*