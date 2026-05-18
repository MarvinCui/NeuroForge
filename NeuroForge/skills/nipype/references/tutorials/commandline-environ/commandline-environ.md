# How To: Commandline Environ

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, mock, workflow, integration

## Overview

Workflow: test Commandline environ

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `simplejson`
- `logging`
- `pytest`
- `unittest`
- `testing`
- `support`
- `nipype.interfaces.ants`
- `nipype`
- `nipype`
- `nipype.interfaces.fsl`

**Setup Required:**
```python
# Fixtures: monkeypatch, tmpdir
```

## Step-by-Step Guide

### Step 1: Call config.set_default_config()

```python
config.set_default_config()
```

**Verification:**
```python
assert res.runtime.environ['DISPLAY'] == ':1'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert 'DISPLAY' not in ci3.inputs.environ
```

### Step 3: Call monkeypatch.setitem()

```python
monkeypatch.setitem(os.environ, 'DISPLAY', ':1')
```

**Verification:**
```python
assert 'DISPLAY' not in res.runtime.environ
```

### Step 4: Assign ci3 = nib.CommandLine(...)

```python
ci3 = nib.CommandLine(command='echo')
```

**Verification:**
```python
assert res.runtime.environ['DISPLAY'] == ':3'
```

### Step 5: Assign res = ci3.run(...)

```python
res = ci3.run()
```

**Verification:**
```python
assert res.runtime.environ['DISPLAY'] == ':2'
```

### Step 6: Call monkeypatch.delitem()

```python
monkeypatch.delitem(os.environ, 'DISPLAY', raising=False)
```

### Step 7: Call config.set()

```python
config.set('execution', 'display_variable', ':3')
```

### Step 8: Assign res = ci3.run(...)

```python
res = ci3.run()
```

**Verification:**
```python
assert 'DISPLAY' not in ci3.inputs.environ
```

### Step 9: Assign ci3._redirect_x = True

```python
ci3._redirect_x = True
```

### Step 10: Assign res = ci3.run(...)

```python
res = ci3.run()
```

**Verification:**
```python
assert res.runtime.environ['DISPLAY'] == ':3'
```

### Step 11: Call monkeypatch.setitem()

```python
monkeypatch.setitem(os.environ, 'DISPLAY', ':1')
```

### Step 12: Assign ci3.inputs.environ = value

```python
ci3.inputs.environ = {'DISPLAY': ':2'}
```

### Step 13: Assign res = ci3.run(...)

```python
res = ci3.run()
```

**Verification:**
```python
assert res.runtime.environ['DISPLAY'] == ':2'
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, tmpdir

# Workflow
from nipype import config
config.set_default_config()
tmpdir.chdir()
monkeypatch.setitem(os.environ, 'DISPLAY', ':1')
ci3 = nib.CommandLine(command='echo')
res = ci3.run()
assert res.runtime.environ['DISPLAY'] == ':1'
monkeypatch.delitem(os.environ, 'DISPLAY', raising=False)
config.set('execution', 'display_variable', ':3')
res = ci3.run()
assert 'DISPLAY' not in ci3.inputs.environ
assert 'DISPLAY' not in res.runtime.environ
ci3._redirect_x = True
res = ci3.run()
assert res.runtime.environ['DISPLAY'] == ':3'
monkeypatch.setitem(os.environ, 'DISPLAY', ':1')
ci3.inputs.environ = {'DISPLAY': ':2'}
res = ci3.run()
assert res.runtime.environ['DISPLAY'] == ':2'
```

## Next Steps


---

*Source: test_core.py:431 | Complexity: Advanced | Last updated: 2026-05-18*