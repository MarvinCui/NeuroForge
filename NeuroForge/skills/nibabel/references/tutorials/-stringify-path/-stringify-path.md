# How To:  Stringify Path

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test  stringify path

## Prerequisites

**Required Modules:**
- `pathlib`
- `pytest`
- `filename_parser`


## Step-by-Step Guide

### Step 1: Assign res = _stringify_path(...)

```python
res = _stringify_path('fname.ext.gz')
```

**Verification:**
```python
assert res == 'fname.ext.gz'
```

### Step 2: Assign res = _stringify_path(...)

```python
res = _stringify_path(pathlib.Path('fname.ext.gz'))
```

**Verification:**
```python
assert res == 'fname.ext.gz'
```

### Step 3: Assign home = pathlib.Path.home.as_posix(...)

```python
home = pathlib.Path.home().as_posix()
```

**Verification:**
```python
assert res == f'{home}/fname.ext.gz'
```

### Step 4: Assign res = _stringify_path(...)

```python
res = _stringify_path(pathlib.Path('~/fname.ext.gz'))
```

**Verification:**
```python
assert res == 'fname.ext.gz'
```

### Step 5: Assign res = _stringify_path(...)

```python
res = _stringify_path(pathlib.Path('./fname.ext.gz'))
```

**Verification:**
```python
assert res == '../fname.ext.gz'
```

### Step 6: Assign res = _stringify_path(...)

```python
res = _stringify_path(pathlib.Path('../fname.ext.gz'))
```

**Verification:**
```python
assert res == '../fname.ext.gz'
```


## Complete Example

```python
# Workflow
res = _stringify_path('fname.ext.gz')
assert res == 'fname.ext.gz'
res = _stringify_path(pathlib.Path('fname.ext.gz'))
assert res == 'fname.ext.gz'
home = pathlib.Path.home().as_posix()
res = _stringify_path(pathlib.Path('~/fname.ext.gz'))
assert res == f'{home}/fname.ext.gz'
res = _stringify_path(pathlib.Path('./fname.ext.gz'))
assert res == 'fname.ext.gz'
res = _stringify_path(pathlib.Path('../fname.ext.gz'))
assert res == '../fname.ext.gz'
```

## Next Steps


---

*Source: test_filename_parser.py:137 | Complexity: Intermediate | Last updated: 2026-05-18*