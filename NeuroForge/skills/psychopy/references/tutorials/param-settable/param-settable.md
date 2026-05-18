# How To: Param Settable

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that all params which are settable each frame/repeat have a set method in the corresponding class.

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

### Step 1: '\n        Check that all params which are settable each frame/repeat have a set method in the corresponding class.\n        '

```python
'\n        Check that all params which are settable each frame/repeat have a set method in the corresponding class.\n        '
```

**Verification:**
```python
assert hasattr(self.libraryClass, methodName), f'Parameter {paramName} can be set {settableStr}, but does not have a method {methodName}'
```

### Step 2: Assign unknown = self.make_minimal_experiment(...)

```python
comp, rt, exp = self.make_minimal_experiment()
```

### Step 3: Assign settable = value

```python
settable = {'repeat': 'set every repeat' in param.allowedUpdates, 'frame': 'set every frame' in param.allowedUpdates}
```

### Step 4: Assign settableList = value

```python
settableList = []
```

### Step 5: Assign settableStr = unknown.join(...)

```python
settableStr = ' or '.join(settableList)
```

### Step 6: Assign methodName = value

```python
methodName = 'set' + BaseComponent._getParamCaps(comp, paramName)
```

**Verification:**
```python
assert hasattr(self.libraryClass, methodName), f'Parameter {paramName} can be set {settableStr}, but does not have a method {methodName}'
```

### Step 7: Call settableList.append()

```python
settableList.append(f'every {key}')
```


## Complete Example

```python
# Workflow
'\n        Check that all params which are settable each frame/repeat have a set method in the corresponding class.\n        '
comp, rt, exp = self.make_minimal_experiment()
for paramName, param in comp.params.items():
    if not param.direct:
        continue
    if param.allowedUpdates is None:
        continue
    settable = {'repeat': 'set every repeat' in param.allowedUpdates, 'frame': 'set every frame' in param.allowedUpdates}
    if any(settable.values()):
        settableList = []
        for key in settable:
            if settable[key]:
                settableList.append(f'every {key}')
        settableStr = ' or '.join(settableList)
        methodName = 'set' + BaseComponent._getParamCaps(comp, paramName)
        assert hasattr(self.libraryClass, methodName), f'Parameter {paramName} can be set {settableStr}, but does not have a method {methodName}'
```

## Next Steps


---

*Source: test_base_components.py:370 | Complexity: Intermediate | Last updated: 2026-05-18*