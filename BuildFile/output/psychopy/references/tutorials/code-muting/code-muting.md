# How To: Code Muting

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that routines are only written when enabled and targets match.

## Prerequisites

**Required Modules:**
- `pathlib`
- `pytest`
- `psychopy`
- `psychopy.hardware`


## Step-by-Step Guide

### Step 1: '\n        Test that routines are only written when enabled and targets match.\n        '

```python
'\n        Test that routines are only written when enabled and targets match.\n        '
```

**Verification:**
```python
assert rt.name in pyScript, f'{type(rt).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
```

### Step 2: Assign unknown = _make_minimal_experiment(...)

```python
rt, exp = _make_minimal_experiment(self)
```

**Verification:**
```python
assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when enabled but PsychoPy not in targets.'
```

### Step 3: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

**Verification:**
```python
assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when disabled but PsychoPy in targets.'
```

### Step 4: Assign unknown.val = True

```python
rt.params['disabled'].val = True
```

**Verification:**
```python
assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when disabled and PsychoPy not in targets.'
```

### Step 5: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

**Verification:**
```python
assert rt.name in pyScript, f'{type(rt).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
```


## Complete Example

```python
# Workflow
'\n        Test that routines are only written when enabled and targets match.\n        '
rt, exp = _make_minimal_experiment(self)
pyScript = exp.writeScript(target='PsychoPy')
if 'PsychoPy' in type(rt).targets:
    assert rt.name in pyScript, f'{type(rt).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
else:
    assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when enabled but PsychoPy not in targets.'
rt.params['disabled'].val = True
pyScript = exp.writeScript(target='PsychoPy')
if 'PsychoPy' in type(rt).targets:
    assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when disabled but PsychoPy in targets.'
else:
    assert rt.name not in pyScript, f'{type(rt).__name__} found in compiled Python script when disabled and PsychoPy not in targets.'
```

## Next Steps


---

*Source: test_base_routine.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*