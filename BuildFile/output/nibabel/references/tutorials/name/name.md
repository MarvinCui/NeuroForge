# How To: Name

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test name

## Prerequisites

**Required Modules:**
- `contextlib`
- `hashlib`
- `os`
- `time`
- `unittest`
- `gzip`
- `io`
- `unittest`
- `pytest`
- `packaging.version`
- `_compression`
- `openers`
- `tmpdirs`
- `indexed_gzip`
- `_compression`


## Step-by-Step Guide

### Step 1: Assign sobj = BytesIO(...)

```python
sobj = BytesIO()
```

**Verification:**
```python
assert fobj.name == exp_name
```

### Step 2: Assign lunk = Lunk(...)

```python
lunk = Lunk('in ART')
```

### Step 3: Assign files_to_test = value

```python
files_to_test = ['test.txt', 'test.txt.gz', 'test.txt.bz2', sobj, lunk]
```

### Step 4: Assign exp_name = value

```python
exp_name = input if type(input) == str else None
```

**Verification:**
```python
assert fobj.name == exp_name
```


## Complete Example

```python
# Workflow
sobj = BytesIO()
lunk = Lunk('in ART')
with InTemporaryDirectory():
    files_to_test = ['test.txt', 'test.txt.gz', 'test.txt.bz2', sobj, lunk]
    if HAVE_ZSTD:
        files_to_test += ['test.txt.zst']
    for input in files_to_test:
        exp_name = input if type(input) == str else None
        with Opener(input, 'wb') as fobj:
            assert fobj.name == exp_name
```

## Next Steps


---

*Source: test_openers.py:282 | Complexity: Intermediate | Last updated: 2026-05-18*