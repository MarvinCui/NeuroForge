# How To: Json Dump And Reopen File

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test json dump and reopen file

## Prerequisites

**Required Modules:**
- `numpy`
- `shutil`
- `json_tricks`
- `tempfile`
- `operator`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`
- `sys`
- `psychopy.data.staircase`


## Step-by-Step Guide

### Step 1: Assign s = data.StairHandler(...)

```python
s = data.StairHandler(5)
```

**Verification:**
```python
assert s == s_loaded
```

### Step 2: Call s.addResponse()

```python
s.addResponse(1)
```

### Step 3: Call s.addOtherData()

```python
s.addOtherData('foo', 'bar')
```

### Step 4: Call s.__next__()

```python
s.__next__()
```

### Step 5: Assign unknown = mkstemp(...)

```python
_, path = mkstemp(dir=self.tmp_dir, suffix='.json')
```

### Step 6: Call s.saveAsJson()

```python
s.saveAsJson(fileName=path, fileCollisionMethod='overwrite')
```

### Step 7: Assign s.origin = ''

```python
s.origin = ''
```

### Step 8: Assign s_loaded = fromFile(...)

```python
s_loaded = fromFile(path)
```

**Verification:**
```python
assert s == s_loaded
```


## Complete Example

```python
# Workflow
s = data.StairHandler(5)
s.addResponse(1)
s.addOtherData('foo', 'bar')
s.__next__()
_, path = mkstemp(dir=self.tmp_dir, suffix='.json')
s.saveAsJson(fileName=path, fileCollisionMethod='overwrite')
s.origin = ''
s_loaded = fromFile(path)
assert s == s_loaded
```

## Next Steps


---

*Source: test_StairHandlers.py:414 | Complexity: Advanced | Last updated: 2026-05-18*