# How To: All Have Depth

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all have depth

## Prerequisites

**Required Modules:**
- `psychopy.experiment.exports`
- `psychopy`
- `inspect`


## Step-by-Step Guide

### Step 1: Assign exceptions = value

```python
exceptions = ('PanoramaComponent', 'FaceAPIComponent')
```

**Verification:**
```python
assert sought in script.replace(' ', ''), f'Could not find any reference to depth in {target} init code for {compName}:\n{script}\nAny component drawn to the screen should be given a `depth` on init. If this component is a special case, you can mark it as exempt by adding it to the `exceptions` variable in this test.\n'
```

### Step 2: Assign exp = experiment.Experiment(...)

```python
exp = experiment.Experiment()
```

### Step 3: Assign rt = experiment.routines.Routine(...)

```python
rt = experiment.routines.Routine(exp=exp, name='testRoutine')
```

### Step 4: Call exp.addRoutine()

```python
exp.addRoutine('testRoutine', rt)
```

### Step 5: Call exp.flow.addRoutine()

```python
exp.flow.addRoutine(rt, 0)
```

### Step 6: Assign comp = compClass(...)

```python
comp = compClass(exp=exp, parentName='testRoutine', name=f'test{compClass.__name__}')
```

### Step 7: Call rt.addComponent()

```python
rt.addComponent(comp)
```

### Step 8: Assign compName = value

```python
compName = type(comp).__name__
```

### Step 9: Assign buff = IndentingBuffer(...)

```python
buff = IndentingBuffer(target=target)
```

### Step 10: Assign script = buff.getvalue(...)

```python
script = buff.getvalue()
```

**Verification:**
```python
assert sought in script.replace(' ', ''), f'Could not find any reference to depth in {target} init code for {compName}:\n{script}\nAny component drawn to the screen should be given a `depth` on init. If this component is a special case, you can mark it as exempt by adding it to the `exceptions` variable in this test.\n'
```

### Step 11: Call comp.writeInitCodeJS()

```python
comp.writeInitCodeJS(buff)
```

### Step 12: Assign sought = 'depth:'

```python
sought = 'depth:'
```

### Step 13: Call comp.writeInitCode()

```python
comp.writeInitCode(buff)
```

### Step 14: Assign sought = 'depth='

```python
sought = 'depth='
```


## Complete Example

```python
# Workflow
exceptions = ('PanoramaComponent', 'FaceAPIComponent')
exp = experiment.Experiment()
rt = experiment.routines.Routine(exp=exp, name='testRoutine')
exp.addRoutine('testRoutine', rt)
exp.flow.addRoutine(rt, 0)
for compName, compClass in experiment.getAllComponents().items():
    if compName in ('SettingsComponent',):
        continue
    comp = compClass(exp=exp, parentName='testRoutine', name=f'test{compClass.__name__}')
    rt.addComponent(comp)
for comp in rt:
    compName = type(comp).__name__
    if compName in exceptions or not isinstance(comp, experiment.components.BaseVisualComponent):
        continue
    for target in ('PsychoPy', 'PsychoJS'):
        if target not in comp.targets:
            continue
        buff = IndentingBuffer(target=target)
        if target == 'PsychoJS':
            comp.writeInitCodeJS(buff)
            sought = 'depth:'
        else:
            comp.writeInitCode(buff)
            sought = 'depth='
        script = buff.getvalue()
        assert sought in script.replace(' ', ''), f'Could not find any reference to depth in {target} init code for {compName}:\n{script}\nAny component drawn to the screen should be given a `depth` on init. If this component is a special case, you can mark it as exempt by adding it to the `exceptions` variable in this test.\n'
```

## Next Steps


---

*Source: test_all_components.py:30 | Complexity: Advanced | Last updated: 2026-05-18*