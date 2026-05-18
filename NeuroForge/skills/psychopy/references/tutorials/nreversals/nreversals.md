# How To: Nreversals

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nReversals

## Prerequisites

**Required Modules:**
- `numpy`
- `shutil`
- `json_tricks`
- `tempfile`
- `operator`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`


## Step-by-Step Guide

### Step 1: Assign start_val = 1

```python
start_val = 1
```

**Verification:**
```python
assert staircase.nReversals == len(step_sizes)
```

### Step 2: Assign step_sizes = list(...)

```python
step_sizes = list(range(5))
```

**Verification:**
```python
assert staircase.nReversals == len(step_sizes)
```

### Step 3: Assign staircase = data.StairHandler(...)

```python
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=None)
```

**Verification:**
```python
assert staircase.nReversals == len(step_sizes) + 1
```

### Step 4: Assign staircase = data.StairHandler(...)

```python
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=len(step_sizes) - 1)
```

**Verification:**
```python
assert staircase.nReversals == len(step_sizes)
```

### Step 5: Assign staircase = data.StairHandler(...)

```python
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=len(step_sizes) + 1)
```

**Verification:**
```python
assert staircase.nReversals == len(step_sizes) + 1
```


## Complete Example

```python
# Workflow
start_val = 1
step_sizes = list(range(5))
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=None)
assert staircase.nReversals == len(step_sizes)
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=len(step_sizes) - 1)
assert staircase.nReversals == len(step_sizes)
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=len(step_sizes) + 1)
assert staircase.nReversals == len(step_sizes) + 1
```

## Next Steps


---

*Source: test_StairHandlers.py:314 | Complexity: Intermediate | Last updated: 2026-05-18*