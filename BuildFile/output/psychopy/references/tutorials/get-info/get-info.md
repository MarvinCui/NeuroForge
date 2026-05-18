# How To: Get Info

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get info

## Prerequisites

**Required Modules:**
- `pathlib`
- `test_base_components`
- `psychopy`
- `utils`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = [{'val': 'randint(0, 999)', 'py': 'randint(0, 999)', 'js': 'util.randint(0, 999)'}]
```

**Verification:**
```python
assert wanted in expInfoStr, f'Could not find `{wanted}` in ```\n{expInfoStr}\n```'
```

### Step 2: Assign exp = experiment.Experiment(...)

```python
exp = experiment.Experiment()
```

### Step 3: Assign unknown.val = '{'

```python
exp.settings.params['Experiment info'].val = '{'
```

### Step 4: Assign i = 0

```python
i = 0
```

### Step 5: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

### Step 6: Assign expInfoStr = value

```python
expInfoStr = pyScript.split('expInfo = {')[1]
```

### Step 7: Assign expInfoStr = value

```python
expInfoStr = expInfoStr.split('}')[0]
```

### Step 8: Assign i = 0

```python
i = 0
```

### Step 9: Assign wanted = value

```python
wanted = f"'{i}': {case['py']},"
```

**Verification:**
```python
assert wanted in expInfoStr, f'Could not find `{wanted}` in ```\n{expInfoStr}\n```'
```


## Complete Example

```python
# Workflow
cases = [{'val': 'randint(0, 999)', 'py': 'randint(0, 999)', 'js': 'util.randint(0, 999)'}]
exp = experiment.Experiment()
exp.settings.params['Experiment info'].val = '{'
i = 0
for case in cases:
    exp.settings.params['Experiment info'].val += f"'{i}': '{case['val']}',"
    i += 1
exp.settings.params['Experiment info'].val += '}'
pyScript = exp.writeScript(target='PsychoPy')
expInfoStr = pyScript.split('expInfo = {')[1]
expInfoStr = expInfoStr.split('}')[0]
i = 0
for case in cases:
    wanted = f"'{i}': {case['py']},"
    assert wanted in expInfoStr, f'Could not find `{wanted}` in ```\n{expInfoStr}\n```'
    i += 1
```

## Next Steps


---

*Source: test_SettingsComponent.py:49 | Complexity: Advanced | Last updated: 2026-05-18*