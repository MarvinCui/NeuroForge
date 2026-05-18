# How To: Var Defs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test var defs

## Prerequisites

**Required Modules:**
- `psychopy.experiment.py2js_transpiler`
- `psychopy.experiment.py2js`
- `psychopy.experiment`
- `psychopy.experiment.components.code`
- `psychopy.experiment.routines`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = [{'py': "'''\nDocstring at line 1\n'''\ncontinueRoutine = False", 'var': False}, {'py': '# Comment at line 1\ncontinueRoutine = False', 'var': False}, {'py': 'continueRoutine = False', 'var': False}, {'py': 'continueRoutine = False\nexpInfo = {}', 'var': False}, {'py': 'sin = None\npi = 3.14', 'var': False}, {'py': 'visual = psychopy.visual\nnp = numpy', 'var': False}, {'py': 'testComponent = None', 'var': False}, {'py': 'testRoutine = None', 'var': False}, {'py': 'newVariable = 0', 'var': True}, {'py': 'continueRoutine = False\nnewVariable = {}', 'var': True}, {'py': 'extantVariable = 0', 'var': True}]
```

**Verification:**
```python
assert 'var ' in jsCode, f'Could not find desired var def in:\n{jsCode}'
```

### Step 2: Assign exp = Experiment(...)

```python
exp = Experiment()
```

**Verification:**
```python
assert 'var ' not in jsCode, f'Found undesired var def in:\n{jsCode}'
```

### Step 3: Assign rt = Routine(...)

```python
rt = Routine('testRoutine', exp)
```

### Step 4: Assign comp = CodeComponent(...)

```python
comp = CodeComponent(exp, parentName='testRoutine', name='testComponent', beforeExp='extantVariable = 1')
```

### Step 5: Call rt.addComponent()

```python
rt.addComponent(comp)
```

### Step 6: Call exp.addRoutine()

```python
exp.addRoutine('testRoutine', rt)
```

### Step 7: Call exp.flow.addRoutine()

```python
exp.flow.addRoutine(rt, 0)
```

### Step 8: Call exp.namespace.add()

```python
exp.namespace.add('testRoutine')
```

### Step 9: Call exp.namespace.add()

```python
exp.namespace.add('testComponent')
```

### Step 10: Assign jsCode = py2js.translatePythonToJavaScript(...)

```python
jsCode = py2js.translatePythonToJavaScript(case['py'], namespace=exp.namespace.all)
```

**Verification:**
```python
assert 'var ' in jsCode, f'Could not find desired var def in:\n{jsCode}'
```


## Complete Example

```python
# Workflow
cases = [{'py': "'''\nDocstring at line 1\n'''\ncontinueRoutine = False", 'var': False}, {'py': '# Comment at line 1\ncontinueRoutine = False', 'var': False}, {'py': 'continueRoutine = False', 'var': False}, {'py': 'continueRoutine = False\nexpInfo = {}', 'var': False}, {'py': 'sin = None\npi = 3.14', 'var': False}, {'py': 'visual = psychopy.visual\nnp = numpy', 'var': False}, {'py': 'testComponent = None', 'var': False}, {'py': 'testRoutine = None', 'var': False}, {'py': 'newVariable = 0', 'var': True}, {'py': 'continueRoutine = False\nnewVariable = {}', 'var': True}, {'py': 'extantVariable = 0', 'var': True}]
exp = Experiment()
rt = Routine('testRoutine', exp)
comp = CodeComponent(exp, parentName='testRoutine', name='testComponent', beforeExp='extantVariable = 1')
rt.addComponent(comp)
exp.addRoutine('testRoutine', rt)
exp.flow.addRoutine(rt, 0)
exp.namespace.add('testRoutine')
exp.namespace.add('testComponent')
for case in cases:
    jsCode = py2js.translatePythonToJavaScript(case['py'], namespace=exp.namespace.all)
    if case['var']:
        assert 'var ' in jsCode, f'Could not find desired var def in:\n{jsCode}'
    else:
        assert 'var ' not in jsCode, f'Found undesired var def in:\n{jsCode}'
```

## Next Steps


---

*Source: test_py2js.py:94 | Complexity: Advanced | Last updated: 2026-05-18*