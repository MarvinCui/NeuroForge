# How To: Indentation Consistency

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.

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

### Step 1: '\n        No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.\n        '

```python
'\n        No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.\n        '
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('init', buff.indentLevel)
```

### Step 2: Assign unknown = self.make_minimal_experiment(...)

```python
comp, rt, exp = self.make_minimal_experiment()
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('routine start', buff.indentLevel)
```

### Step 3: Assign buff = IndentingBuffer(...)

```python
buff = IndentingBuffer(target='PsychoPy')
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('each frame', buff.indentLevel)
```

### Step 4: Assign errMsgTemplate = 'Writing {} code for {} changes indent level by {} when start is `{}` and stop is `{}`.'

```python
errMsgTemplate = 'Writing {} code for {} changes indent level by {} when start is `{}` and stop is `{}`.'
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('routine end', buff.indentLevel)
```

### Step 5: Call exp.flow.writeStartCode()

```python
exp.flow.writeStartCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('experiment end', buff.indentLevel)
```

### Step 6: Assign cases = value

```python
cases = [{'startVal': '0', 'stopVal': '1'}, {'startVal': '', 'stopVal': '1'}, {'startVal': '0', 'stopVal': ''}, {'startVal': '', 'stopVal': ''}]
```

### Step 7: Call pytest.skip()

```python
pytest.skip()
```

### Step 8: Assign errMsg = errMsgTemplate.format(...)

```python
errMsg = errMsgTemplate.format('{}', type(comp).__name__, '{}', case['startVal'], case['stopVal'])
```

### Step 9: Assign unknown.val = 'time (s)'

```python
comp.params['startType'].val = 'time (s)'
```

### Step 10: Assign unknown.val = 'time (s)'

```python
comp.params['stopType'].val = 'time (s)'
```

### Step 11: Call comp.writeInitCode()

```python
comp.writeInitCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('init', buff.indentLevel)
```

### Step 12: Call comp.writeRoutineStartCode()

```python
comp.writeRoutineStartCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('routine start', buff.indentLevel)
```

### Step 13: Call comp.writeFrameCode()

```python
comp.writeFrameCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('each frame', buff.indentLevel)
```

### Step 14: Call comp.writeRoutineEndCode()

```python
comp.writeRoutineEndCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('routine end', buff.indentLevel)
```

### Step 15: Call comp.writeExperimentEndCode()

```python
comp.writeExperimentEndCode(buff)
```

**Verification:**
```python
assert buff.indentLevel == 0, errMsg.format('experiment end', buff.indentLevel)
```

### Step 16: Assign unknown.val = val

```python
comp.params[param].val = val
```


## Complete Example

```python
# Workflow
'\n        No component should exit any of its write methods at a different indent level as it entered, as this would break subsequent components / routines.\n        '
comp, rt, exp = self.make_minimal_experiment()
if 'startVal' not in comp.params or 'stopVal' not in comp.params:
    pytest.skip()
buff = IndentingBuffer(target='PsychoPy')
errMsgTemplate = 'Writing {} code for {} changes indent level by {} when start is `{}` and stop is `{}`.'
exp.flow.writeStartCode(buff)
cases = [{'startVal': '0', 'stopVal': '1'}, {'startVal': '', 'stopVal': '1'}, {'startVal': '0', 'stopVal': ''}, {'startVal': '', 'stopVal': ''}]
for case in cases:
    errMsg = errMsgTemplate.format('{}', type(comp).__name__, '{}', case['startVal'], case['stopVal'])
    comp.params['startType'].val = 'time (s)'
    comp.params['stopType'].val = 'time (s)'
    for param, val in case.items():
        comp.params[param].val = val
    comp.writeInitCode(buff)
    assert buff.indentLevel == 0, errMsg.format('init', buff.indentLevel)
    comp.writeRoutineStartCode(buff)
    assert buff.indentLevel == 0, errMsg.format('routine start', buff.indentLevel)
    comp.writeFrameCode(buff)
    assert buff.indentLevel == 0, errMsg.format('each frame', buff.indentLevel)
    comp.writeRoutineEndCode(buff)
    assert buff.indentLevel == 0, errMsg.format('routine end', buff.indentLevel)
    comp.writeExperimentEndCode(buff)
    assert buff.indentLevel == 0, errMsg.format('experiment end', buff.indentLevel)
```

## Next Steps


---

*Source: test_base_components.py:102 | Complexity: Advanced | Last updated: 2026-05-18*