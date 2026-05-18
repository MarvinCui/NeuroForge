# How To: Disabled Code Muting

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that components are only written when enabled and targets match.

## Prerequisites

**Required Modules:**
- `ast`
- `esprima`
- `re`
- `pathlib`
- `esprima.error_handler`
- `pytest`
- `tempfile`
- `psychopy`
- `psychopy.experiment.loops`
- `psychopy.experiment.components`
- `psychopy.experiment.exports`
- `psychopy.constants`
- `psychopy.tests`
- `psychopy.hardware`


## Step-by-Step Guide

### Step 1: '\n        Test that components are only written when enabled and targets match.\n        '

```python
'\n        Test that components are only written when enabled and targets match.\n        '
```

**Verification:**
```python
assert comp.name in pyScript, f'{type(comp).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
```

### Step 2: Assign unknown = self.make_minimal_experiment(...)

```python
comp, rt, exp = self.make_minimal_experiment()
```

**Verification:**
```python
assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when enabled but PsychoPy not in targets.'
```

### Step 3: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

**Verification:**
```python
assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when disabled but PsychoPy in targets.'
```

### Step 4: Assign unknown.val = True

```python
comp.params['disabled'].val = True
```

**Verification:**
```python
assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when disabled and PsychoPy not in targets.'
```

### Step 5: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

### Step 6: Call pytest.skip()

```python
pytest.skip()
```

**Verification:**
```python
assert comp.name in pyScript, f'{type(comp).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
```


## Complete Example

```python
# Workflow
'\n        Test that components are only written when enabled and targets match.\n        '
if self.comp.__name__ == 'CodeComponent':
    pytest.skip()
comp, rt, exp = self.make_minimal_experiment()
pyScript = exp.writeScript(target='PsychoPy')
if 'PsychoPy' in type(comp).targets:
    assert comp.name in pyScript, f'{type(comp).__name__} not found in compiled Python script when enabled and PsychoPy in targets.'
else:
    assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when enabled but PsychoPy not in targets.'
comp.params['disabled'].val = True
pyScript = exp.writeScript(target='PsychoPy')
if 'PsychoPy' in type(comp).targets:
    assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when disabled but PsychoPy in targets.'
else:
    assert comp.name not in pyScript, f'{type(comp).__name__} found in compiled Python script when disabled and PsychoPy not in targets.'
```

## Next Steps


---

*Source: test_base_components.py:231 | Complexity: Intermediate | Last updated: 2026-05-18*