# How To: Writing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test writing

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `unittest`
- `subprocess`
- `shutil`
- `pathlib`
- `psychopy`
- `psychopy.tools.versionchooser`
- `psychopy`
- `psychopy.scripts.psyexpCompile`
- `psychopy.experiment.components`
- `tempfile`


## Step-by-Step Guide

### Step 1: Assign exp = experiment.Experiment(...)

```python
exp = experiment.Experiment()
```

**Verification:**
```python
assert 'anchor' not in args, "When compiling Py with useversion 2021.1.4, found 'anchor' argument in ShapeStim; this was not implemented in requested version."
```

### Step 2: Assign rt = experiment.routines.Routine(...)

```python
rt = experiment.routines.Routine(name='testRoutine', exp=exp)
```

**Verification:**
```python
assert "import { PsychoJS } from './lib/core-2021.1.4.js'" in script, 'When compiling JS with useversion 2021.1.4, could not find version-specific import statement.'
```

### Step 3: Call exp.addRoutine()

```python
exp.addRoutine('testRoutine', rt)
```

### Step 4: Call exp.flow.addRoutine()

```python
exp.flow.addRoutine(rt, 0)
```

### Step 5: Assign comp = polygon.PolygonComponent(...)

```python
comp = polygon.PolygonComponent(exp=exp, parentName='testRoutine')
```

### Step 6: Call rt.addComponent()

```python
rt.addComponent(comp)
```

### Step 7: Assign unknown.val = '2021.1.4'

```python
exp.settings.params['Use version'].val = '2021.1.4'
```

### Step 8: Call exp.saveToXML()

```python
exp.saveToXML(str(self.temp / 'versionText.psyexp'))
```

### Step 9: Assign scriptFile = str(...)

```python
scriptFile = str(self.temp / 'versionText.py')
```

### Step 10: Call generateScript()

```python
generateScript(outfile=scriptFile, exp=exp, target='PsychoPy')
```

### Step 11: Assign args = value

```python
args = script.split(f'{comp.name} = visual.ShapeStim(')[1]
```

### Step 12: Assign args = value

```python
args = args.split(')')[0]
```

**Verification:**
```python
assert 'anchor' not in args, "When compiling Py with useversion 2021.1.4, found 'anchor' argument in ShapeStim; this was not implemented in requested version."
```

### Step 13: Assign scriptFile = str(...)

```python
scriptFile = str(self.temp / 'versionText.js')
```

### Step 14: Call generateScript()

```python
generateScript(outfile=scriptFile, exp=exp, target='PsychoJS')
```

**Verification:**
```python
assert "import { PsychoJS } from './lib/core-2021.1.4.js'" in script, 'When compiling JS with useversion 2021.1.4, could not find version-specific import statement.'
```

### Step 15: Assign script = f.read(...)

```python
script = f.read()
```

### Step 16: Assign script = f.read(...)

```python
script = f.read()
```


## Complete Example

```python
# Workflow
if pyVersion > Version('3.6'):
    return
exp = experiment.Experiment()
rt = experiment.routines.Routine(name='testRoutine', exp=exp)
exp.addRoutine('testRoutine', rt)
exp.flow.addRoutine(rt, 0)
comp = polygon.PolygonComponent(exp=exp, parentName='testRoutine')
rt.addComponent(comp)
exp.settings.params['Use version'].val = '2021.1.4'
exp.saveToXML(str(self.temp / 'versionText.psyexp'))
scriptFile = str(self.temp / 'versionText.py')
generateScript(outfile=scriptFile, exp=exp, target='PsychoPy')
with open(scriptFile, 'r') as f:
    script = f.read()
args = script.split(f'{comp.name} = visual.ShapeStim(')[1]
args = args.split(')')[0]
assert 'anchor' not in args, "When compiling Py with useversion 2021.1.4, found 'anchor' argument in ShapeStim; this was not implemented in requested version."
scriptFile = str(self.temp / 'versionText.js')
generateScript(outfile=scriptFile, exp=exp, target='PsychoJS')
with open(scriptFile, 'r') as f:
    script = f.read()
assert "import { PsychoJS } from './lib/core-2021.1.4.js'" in script, 'When compiling JS with useversion 2021.1.4, could not find version-specific import statement.'
```

## Next Steps


---

*Source: test_versionchooser.py:42 | Complexity: Advanced | Last updated: 2026-05-18*