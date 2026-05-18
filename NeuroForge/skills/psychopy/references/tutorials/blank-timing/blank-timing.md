# How To: Blank Timing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that this Component can handle blank start/stop values.

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

### Step 1: '\n        Check that this Component can handle blank start/stop values.\n        '

```python
'\n        Check that this Component can handle blank start/stop values.\n        '
```

**Verification:**
```python
assert startTime == case['startTime']
```

### Step 2: Assign unknown = self.make_minimal_experiment(...)

```python
comp, rt, exp = self.make_minimal_experiment()
```

**Verification:**
```python
assert duration == case['duration']
```

### Step 3: Assign unknown.val = 'time (s)'

```python
comp.params['startType'].val = 'time (s)'
```

**Verification:**
```python
assert not nonSlipSafe
```

### Step 4: Assign unknown.val = 'duration (s)'

```python
comp.params['stopType'].val = 'duration (s)'
```

### Step 5: Assign cases = value

```python
cases = [{'name': 'NoStart', 'startVal': '', 'stopVal': '1', 'startTime': None, 'duration': 1}, {'name': 'NoStop', 'startVal': '0', 'stopVal': '', 'startTime': 0, 'duration': FOREVER}, {'name': 'NoStartStop', 'startVal': '', 'stopVal': '', 'startTime': None, 'duration': FOREVER}]
```

### Step 6: Call pytest.skip()

```python
pytest.skip()
```

### Step 7: Assign unknown.val = value

```python
comp.params['startVal'].val = case['startVal']
```

### Step 8: Assign unknown.val = value

```python
comp.params['stopVal'].val = case['stopVal']
```

### Step 9: Assign unknown = comp.getStartAndDuration(...)

```python
startTime, duration, nonSlipSafe = comp.getStartAndDuration()
```

**Verification:**
```python
assert startTime == case['startTime']
```

### Step 10: Assign unknown = value

```python
case['name'] = self.comp.__name__ + case['name']
```

### Step 11: Assign exp.name = value

```python
exp.name = 'Test%(name)sExp' % case
```

### Step 12: Call pytest.skip()

```python
pytest.skip()
```

### Step 13: Call utils.checkSyntax()

```python
utils.checkSyntax(exp, targets=self.comp.targets)
```

### Step 14: Assign unknown = err

```python
case['err'] = err
```


## Complete Example

```python
# Workflow
'\n        Check that this Component can handle blank start/stop values.\n        '
comp, rt, exp = self.make_minimal_experiment()
for key in ('startVal', 'startType', 'stopVal', 'stopType'):
    if key not in comp.params:
        pytest.skip()
if type(comp).__name__ == 'StaticComponent':
    pytest.skip()
comp.params['startType'].val = 'time (s)'
comp.params['stopType'].val = 'duration (s)'
cases = [{'name': 'NoStart', 'startVal': '', 'stopVal': '1', 'startTime': None, 'duration': 1}, {'name': 'NoStop', 'startVal': '0', 'stopVal': '', 'startTime': 0, 'duration': FOREVER}, {'name': 'NoStartStop', 'startVal': '', 'stopVal': '', 'startTime': None, 'duration': FOREVER}]
for case in cases:
    comp.params['startVal'].val = case['startVal']
    comp.params['stopVal'].val = case['stopVal']
    startTime, duration, nonSlipSafe = comp.getStartAndDuration()
    assert startTime == case['startTime']
    assert duration == case['duration']
    assert not nonSlipSafe
    case['name'] = self.comp.__name__ + case['name']
    exp.name = 'Test%(name)sExp' % case
    try:
        utils.checkSyntax(exp, targets=self.comp.targets)
    except SyntaxError as err:
        case['err'] = err
        raise AssertionError("Syntax error in compiled Builder code when startVal was '%(startVal)s' and stopVal was '%(stopVal)s'. Failed script saved in psychopy/tests/fails. Original error: %(err)s" % case)
```

## Next Steps


---

*Source: test_base_components.py:166 | Complexity: Advanced | Last updated: 2026-05-18*