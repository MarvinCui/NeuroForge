# How To: Exp Loadcompilepsyexp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Exp LoadCompilePsyexp

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

### Step 1: Assign exp = value

```python
exp = self.exp
```

**Verification:**
```python
assert not diff_in_file_py
```

### Step 2: Assign self.new_diff_file = value

```python
self.new_diff_file = self.tmp_diffs_file
```

### Step 3: Assign test_psyexp = list(...)

```python
test_psyexp = list(glob.glob(path.join(self.tmp_dir, '*.psyexp')))
```

### Step 4: Assign diff_in_file_py = ''

```python
diff_in_file_py = ''
```

### Step 5: Call locale.setlocale()

```python
locale.setlocale(locale.LC_ALL, '')
```

**Verification:**
```python
assert not diff_in_file_py
```

### Step 6: Call pytest.skip()

```python
pytest.skip('No test .psyexp files found (no Builder demos??)')
```

### Step 7: Assign testlocList = value

```python
testlocList = ['en_US', 'en_US.UTF-8', 'ja_JP']
```

### Step 8: Assign testlocList = value

```python
testlocList = ['USA', 'JPN']
```

### Step 9: Assign unknown = self._checkLoadSave(...)

```python
file_py, file_psyexp = self._checkLoadSave(file)
```

### Step 10: Assign file_pyc = self._checkCompile(...)

```python
file_pyc = self._checkCompile(file_py)
```

### Step 11: Assign unknown = self._checkLoadSave(...)

```python
file2_py, file2_psyexp = self._checkLoadSave(file_psyexp)
```

### Step 12: Assign file2_pyc = self._checkCompile(...)

```python
file2_pyc = self._checkCompile(file2_py)
```

### Step 13: Assign d = self._checkPyDiff(...)

```python
d = self._checkPyDiff(file_py, file2_py)
```

### Step 14: Call shutil.copyfile()

```python
shutil.copyfile(path.join(root, f), path.join(self.tmp_dir, f))
```

### Step 15: Call locale.setlocale()

```python
locale.setlocale(locale.LC_ALL, loc)
```


## Complete Example

```python
# Workflow
exp = self.exp
self.new_diff_file = self.tmp_diffs_file
for root, dirs, files in os.walk(path.join(self.exp.prefsPaths['demos'], 'builder')):
    for f in files:
        if (f.endswith('.psyexp') or f.endswith('.xlsx') or f.endswith('.csv')) and (not f.startswith('bart')):
            shutil.copyfile(path.join(root, f), path.join(self.tmp_dir, f))
test_psyexp = list(glob.glob(path.join(self.tmp_dir, '*.psyexp')))
if len(test_psyexp) == 0:
    pytest.skip('No test .psyexp files found (no Builder demos??)')
diff_in_file_py = ''
locale.setlocale(locale.LC_ALL, '')
if not sys.platform.startswith('win'):
    testlocList = ['en_US', 'en_US.UTF-8', 'ja_JP']
else:
    testlocList = ['USA', 'JPN']
for file in test_psyexp:
    for loc in ['en_US', 'ja_JP']:
        try:
            locale.setlocale(locale.LC_ALL, loc)
        except locale.Error:
            continue
        file_py, file_psyexp = self._checkLoadSave(file)
        file_pyc = self._checkCompile(file_py)
        file2_py, file2_psyexp = self._checkLoadSave(file_psyexp)
        file2_pyc = self._checkCompile(file2_py)
        d = self._checkPyDiff(file_py, file2_py)
        if d:
            diff_in_file_py += os.path.basename(file) + '::' + d
assert not diff_in_file_py
```

## Next Steps


---

*Source: test_Experiment.py:159 | Complexity: Advanced | Last updated: 2026-05-18*