# How To: Run Faststrooppsyexp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Run FastStroopPsyExp

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy.experiment`
- `psychopy.experiment.components.text`
- `psychopy.experiment._experiment`
- `psychopy.tests.utils`
- `os`
- `os`
- `shutil`
- `glob`
- `py_compile`
- `difflib`
- `tempfile`
- `codecs`
- `psychopy`
- `pytest`
- `locale`
- `numpy`
- `sys`
- `re`
- `xmlschema`
- `psychopy.experiment`


## Step-by-Step Guide

### Step 1: Assign expfile = path.join(...)

```python
expfile = path.join(self.exp.prefsPaths['tests'], 'data', 'ghost_stroop.psyexp')
```

**Verification:**
```python
assert not stderr
```

### Step 2: Call shutil.copyfile()

```python
shutil.copyfile(os.path.join(self.exp.prefsPaths['tests'], 'data', 'ghost_trialTypes.xlsx'), os.path.join(self.tmp_dir, 'ghost_trialTypes.xlsx'))
```

### Step 3: Assign text = text.replace(...)

```python
text = text.replace("'Arial'", "'" + TESTS_FONT + "'")
```

### Step 4: Assign expfile = path.join(...)

```python
expfile = path.join(self.tmp_dir, 'ghost_stroop.psyexp')
```

### Step 5: Call self.exp.loadFromXML()

```python
self.exp.loadFromXML(expfile)
```

### Step 6: Assign unknown.val = os.path.abspath(...)

```python
self.exp.settings.params['Saved data folder'].val = os.path.abspath(self.tmp_dir)
```

### Step 7: Assign unknown.valType = 'str'

```python
self.exp.settings.params['Saved data folder'].valType = 'str'
```

### Step 8: Assign script = self.exp.writeScript(...)

```python
script = self.exp.writeScript()
```

### Step 9: Assign script = script.replace(...)

```python
script = script.replace('fullscr=False,', 'pos=(40,40), fullscr=False,')
```

### Step 10: Assign script = script.replace(...)

```python
script = script.replace('logging.console.setLevel(logging.WARNING', 'logging.console.setLevel(logging.ERROR')
```

### Step 11: Assign lastrun = path.join(...)

```python
lastrun = path.join(self.tmp_dir, 'ghost_stroop_lastrun.py')
```

### Step 12: Assign unknown = core.shellCall(...)

```python
stdout, stderr = core.shellCall([sys.executable, lastrun], stderr=True)
```

**Verification:**
```python
assert not stderr
```

### Step 13: Call pytest.skip()

```python
pytest.skip('response emulation thread not working on linux yet')
```

### Step 14: Assign text = f.read(...)

```python
text = f.read()
```

### Step 15: Call f.write()

```python
f.write(text)
```

### Step 16: Call f.write()

```python
f.write(script)
```


## Complete Example

```python
# Workflow
if sys.platform.startswith('linux'):
    pytest.skip('response emulation thread not working on linux yet')
expfile = path.join(self.exp.prefsPaths['tests'], 'data', 'ghost_stroop.psyexp')
with codecs.open(expfile, 'r', encoding='utf-8-sig') as f:
    text = f.read()
shutil.copyfile(os.path.join(self.exp.prefsPaths['tests'], 'data', 'ghost_trialTypes.xlsx'), os.path.join(self.tmp_dir, 'ghost_trialTypes.xlsx'))
text = text.replace("'Arial'", "'" + TESTS_FONT + "'")
expfile = path.join(self.tmp_dir, 'ghost_stroop.psyexp')
with codecs.open(expfile, 'w', encoding='utf-8-sig') as f:
    f.write(text)
self.exp.loadFromXML(expfile)
self.exp.settings.params['Saved data folder'].val = os.path.abspath(self.tmp_dir)
self.exp.settings.params['Saved data folder'].valType = 'str'
script = self.exp.writeScript()
script = script.replace('fullscr=False,', 'pos=(40,40), fullscr=False,')
script = script.replace('logging.console.setLevel(logging.WARNING', 'logging.console.setLevel(logging.ERROR')
lastrun = path.join(self.tmp_dir, 'ghost_stroop_lastrun.py')
with codecs.open(lastrun, 'w', encoding='utf-8-sig') as f:
    f.write(script)
stdout, stderr = core.shellCall([sys.executable, lastrun], stderr=True)
assert not stderr
```

## Next Steps


---

*Source: test_Experiment.py:219 | Complexity: Advanced | Last updated: 2026-05-18*