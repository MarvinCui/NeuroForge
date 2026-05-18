# How To: All Code Component Tabs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all code component tabs

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `psychopy`
- `psychopy.experiment.loops`
- `psychopy.experiment.routines`
- `psychopy.experiment.components.code`
- `psychopy.tests.utils`


## Step-by-Step Guide

### Step 1: Assign unknown = self.make_minimal_experiment(...)

```python
comp, rt, exp = self.make_minimal_experiment()
```

**Verification:**
```python
assert marker in script, f'Could not find {marker} in {lang} script.'
```

### Step 2: Assign tabs = value

```python
tabs = {'Before Experiment': '___before_experiment___', 'Begin Experiment': '___begin_experiment___', 'Begin Routine': '___begin_routine___', 'Each Frame': '___each_frame___', 'End Routine': '___end_routine___', 'End Experiment': '___end_experiment___'}
```

**Verification:**
```python
assert script.find('___before_experiment___') < script.find('___begin_experiment___') < script.find('___begin_routine___') < script.find('___each_frame___') < script.find('___end_routine___') < script.find('___end_experiment___')
```

### Step 3: Assign pyScript = exp.writeScript(...)

```python
pyScript = exp.writeScript(target='PsychoPy')
```

**Verification:**
```python
assert script.find('___before_experiment___') < script.find('visual.Window') < script.find('___begin_experiment___') < script.find('continueRoutine = True')
```

### Step 4: Assign jsScript = exp.writeScript(...)

```python
jsScript = exp.writeScript(target='PsychoJS')
```

**Verification:**
```python
assert script.find('continueRoutine = True') < script.find('___begin_routine___') < script.find('while continueRoutine:') < script.find('___each_frame___')
```

### Step 5: Assign jsParamName = paramName.replace(...)

```python
jsParamName = paramName.replace(' ', ' JS ')
```

**Verification:**
```python
assert script.find('thisComponent.setAutoDraw(False)') < script.find('___end_routine___') < script.find('routineTimer.reset()') < script.find('___end_experiment___')
```

### Step 6: Assign unknown.val, unknown.val = unknown.join(...)

```python
comp.params[paramName].val = comp.params[jsParamName].val = ' = '.join([self.comp.__name__, comp.name, marker])
```

**Verification:**
```python
assert script.find('___before_experiment___') < script.find('___begin_experiment___') < script.find('___begin_routine___') < script.find('___each_frame___') < script.find('___end_routine___') < script.find('___end_experiment___')
```

### Step 7: Assign ext = value

```python
ext = '.py' if lang == 'Python' else '.js'
```

### Step 8: Call f.write()

```python
f.write(script)
```


## Complete Example

```python
# Workflow
comp, rt, exp = self.make_minimal_experiment()
tabs = {'Before Experiment': '___before_experiment___', 'Begin Experiment': '___begin_experiment___', 'Begin Routine': '___begin_routine___', 'Each Frame': '___each_frame___', 'End Routine': '___end_routine___', 'End Experiment': '___end_experiment___'}
for paramName, marker in tabs.items():
    jsParamName = paramName.replace(' ', ' JS ')
    comp.params[paramName].val = comp.params[jsParamName].val = ' = '.join([self.comp.__name__, comp.name, marker])
pyScript = exp.writeScript(target='PsychoPy')
jsScript = exp.writeScript(target='PsychoJS')
for lang, script in {'Python': pyScript, 'JS': jsScript}.items():
    for paramName, marker in tabs.items():
        try:
            assert marker in script, f'Could not find {marker} in {lang} script.'
        except AssertionError as err:
            ext = '.py' if lang == 'Python' else '.js'
            with open(Path(TESTS_DATA_PATH) / ('test_all_code_component_tabs_local' + ext), 'w') as f:
                f.write(script)
            raise err
    if lang == 'Python':
        assert script.find('___before_experiment___') < script.find('___begin_experiment___') < script.find('___begin_routine___') < script.find('___each_frame___') < script.find('___end_routine___') < script.find('___end_experiment___')
        assert script.find('___before_experiment___') < script.find('visual.Window') < script.find('___begin_experiment___') < script.find('continueRoutine = True')
        assert script.find('continueRoutine = True') < script.find('___begin_routine___') < script.find('while continueRoutine:') < script.find('___each_frame___')
        assert script.find('thisComponent.setAutoDraw(False)') < script.find('___end_routine___') < script.find('routineTimer.reset()') < script.find('___end_experiment___')
```

## Next Steps


---

*Source: test_CodeComponent.py:26 | Complexity: Advanced | Last updated: 2026-05-18*