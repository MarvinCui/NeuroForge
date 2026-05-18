# How To: Getfuturetrials

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that TrialHandler2 can return future trials correctly.

## Prerequisites

**Required Modules:**
- `os`
- `glob`
- `os.path`
- `shutil`
- `tempfile`
- `numpy`
- `io`
- `json_tricks`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: '\n        Check that TrialHandler2 can return future trials correctly.\n        '

```python
'\n        Check that TrialHandler2 can return future trials correctly.\n        '
```

**Verification:**
```python
assert getattr(trial, key) == answers[n][key]
```

### Step 2: Assign t = data.TrialHandler2(...)

```python
t = data.TrialHandler2(self.conditions, nReps=2, method='sequential')
```

**Verification:**
```python
assert answers[n] is None
```

### Step 3: Assign up1 = t.getFutureTrial(...)

```python
up1 = t.getFutureTrial(1)
```

**Verification:**
```python
assert trials[i] == t.upcomingTrials[i]
```

### Step 4: Assign ups3 = t.getFutureTrials(...)

```python
ups3 = t.getFutureTrials(3)
```

### Step 5: Call t.__next__()

```python
t.__next__()
```

### Step 6: Assign answers = value

```python
answers = [{'thisN': 5, 'thisRepN': 1, 'thisTrialN': 2, 'thisIndex': 2}, {'thisN': 1, 'thisRepN': 0, 'thisTrialN': 1, 'thisIndex': 1}, {'thisN': 2, 'thisRepN': 0, 'thisTrialN': 2, 'thisIndex': 2}, {'thisN': 3, 'thisRepN': 1, 'thisTrialN': 0, 'thisIndex': 0}, {'thisN': 4, 'thisRepN': 1, 'thisTrialN': 1, 'thisIndex': 1}, {'thisN': 5, 'thisRepN': 1, 'thisTrialN': 2, 'thisIndex': 2}, None]
```

### Step 7: Assign trials = t.getFutureTrials(...)

```python
trials = t.getFutureTrials(None)
```

### Step 8: Assign trial = t.getFutureTrial(...)

```python
trial = t.getFutureTrial(n)
```

**Verification:**
```python
assert trials[i] == t.upcomingTrials[i]
```


## Complete Example

```python
# Workflow
'\n        Check that TrialHandler2 can return future trials correctly.\n        '
t = data.TrialHandler2(self.conditions, nReps=2, method='sequential')
up1 = t.getFutureTrial(1)
ups3 = t.getFutureTrials(3)
t.__next__()
answers = [{'thisN': 5, 'thisRepN': 1, 'thisTrialN': 2, 'thisIndex': 2}, {'thisN': 1, 'thisRepN': 0, 'thisTrialN': 1, 'thisIndex': 1}, {'thisN': 2, 'thisRepN': 0, 'thisTrialN': 2, 'thisIndex': 2}, {'thisN': 3, 'thisRepN': 1, 'thisTrialN': 0, 'thisIndex': 0}, {'thisN': 4, 'thisRepN': 1, 'thisTrialN': 1, 'thisIndex': 1}, {'thisN': 5, 'thisRepN': 1, 'thisTrialN': 2, 'thisIndex': 2}, None]
for n in range(7):
    trial = t.getFutureTrial(n)
    if trial is not None:
        for key in answers[n]:
            assert getattr(trial, key) == answers[n][key]
    else:
        assert answers[n] is None
trials = t.getFutureTrials(None)
for i in range(len(trials)):
    assert trials[i] == t.upcomingTrials[i]
```

## Next Steps


---

*Source: test_TrialHandler2.py:310 | Complexity: Advanced | Last updated: 2026-05-18*