# How To: Applyinitialrule False

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test applyInitialRule False

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

### Step 1: Assign start_val = 10

```python
start_val = 10
```

**Verification:**
```python
assert staircase.data == responses
```

### Step 2: Assign step_sizes = 2

```python
step_sizes = 2
```

**Verification:**
```python
assert staircase.intensities == intensities
```

### Step 3: Assign staircase = data.StairHandler(...)

```python
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=2, nUp=1, nDown=2, applyInitialRule=False, stepType='lin')
```

### Step 4: Assign responses = value

```python
responses = [0, 1, 1, 0]
```

### Step 5: Assign intensities = value

```python
intensities = [10, 12, 12, 10]
```

**Verification:**
```python
assert staircase.data == responses
```

### Step 6: Call staircase.__next__()

```python
staircase.__next__()
```

### Step 7: Call staircase.addResponse()

```python
staircase.addResponse(r)
```


## Complete Example

```python
# Workflow
start_val = 10
step_sizes = 2
staircase = data.StairHandler(startVal=start_val, stepSizes=step_sizes, nReversals=2, nUp=1, nDown=2, applyInitialRule=False, stepType='lin')
responses = [0, 1, 1, 0]
intensities = [10, 12, 12, 10]
for r in responses:
    try:
        staircase.__next__()
        staircase.addResponse(r)
    except StopIteration:
        break
assert staircase.data == responses
assert staircase.intensities == intensities
```

## Next Steps


---

*Source: test_StairHandlers.py:330 | Complexity: Advanced | Last updated: 2026-05-18*