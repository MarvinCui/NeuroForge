# How To: Visual Set Autodraw

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that any components derived from BaseVisualComponent make some reference to `.autoDraw` in their each
frame code

## Prerequisites

**Required Modules:**
- `psychopy.experiment.exports`
- `psychopy`
- `inspect`


## Step-by-Step Guide

### Step 1: '\n    Check that any components derived from BaseVisualComponent make some reference to `.autoDraw` in their each\n    frame code\n    '

```python
'\n    Check that any components derived from BaseVisualComponent make some reference to `.autoDraw` in their each\n    frame code\n    '
```

**Verification:**
```python
assert '.autoDraw = ' in code or '.setAutoDraw(' in code, f'{compName} does not set autoDraw in its Each Frame code. If this is acceptable, add the component name to `skipComponents`.'
```

### Step 2: Assign skipComponents = value

```python
skipComponents = ['ApertureComponent']
```

### Step 3: Assign tester = value

```python
tester = _Generic(compClass).comp
```

### Step 4: Assign buff = IndentingBuffer(...)

```python
buff = IndentingBuffer(target='PsychoPy')
```

### Step 5: Call tester.writeFrameCode()

```python
tester.writeFrameCode(buff)
```

### Step 6: Assign code = buff.getvalue(...)

```python
code = buff.getvalue()
```

**Verification:**
```python
assert '.autoDraw = ' in code or '.setAutoDraw(' in code, f'{compName} does not set autoDraw in its Each Frame code. If this is acceptable, add the component name to `skipComponents`.'
```

### Step 7: Assign unknown.val = 0

```python
tester.params['startVal'].val = 0
```

### Step 8: Assign unknown.val = 1

```python
tester.params['stopVal'].val = 1
```


## Complete Example

```python
# Workflow
'\n    Check that any components derived from BaseVisualComponent make some reference to `.autoDraw` in their each\n    frame code\n    '
skipComponents = ['ApertureComponent']
for compName, compClass in experiment.getAllComponents().items():
    if compName in skipComponents:
        continue
    if not issubclass(compClass, experiment.components.BaseVisualComponent):
        continue
    tester = _Generic(compClass).comp
    if 'startVal' in tester.params:
        tester.params['startVal'].val = 0
    if 'stopVal' in tester.params:
        tester.params['stopVal'].val = 1
    buff = IndentingBuffer(target='PsychoPy')
    tester.writeFrameCode(buff)
    code = buff.getvalue()
    assert '.autoDraw = ' in code or '.setAutoDraw(' in code, f'{compName} does not set autoDraw in its Each Frame code. If this is acceptable, add the component name to `skipComponents`.'
```

## Next Steps


---

*Source: test_all_components.py:74 | Complexity: Advanced | Last updated: 2026-05-18*