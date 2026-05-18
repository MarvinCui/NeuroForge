# How To: Cifs Check

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test cifs check

## Prerequisites

**Required Modules:**
- `os`
- `time`
- `pathlib`
- `unittest`
- `pytest`
- `testing`
- `utils.filemanip`


## Step-by-Step Guide

### Step 1: Assign fake_table = value

```python
fake_table = [('/scratch/tmp', 'ext4'), ('/scratch', 'cifs')]
```

**Verification:**
```python
assert isinstance(_cifs_table, list)
```

### Step 2: Assign cifs_targets = value

```python
cifs_targets = [('/scratch/tmp/x/y', False), ('/scratch/tmp/x', False), ('/scratch/x/y', True), ('/scratch/x', True), ('/x/y', False), ('/x', False), ('/', False)]
```

**Verification:**
```python
assert isinstance(on_cifs('/'), bool)
```

### Step 3: Assign orig_table = value

```python
orig_table = _cifs_table[:]
```

**Verification:**
```python
assert on_cifs(target) is False
```

### Step 4: Assign unknown = value

```python
_cifs_table[:] = []
```

**Verification:**
```python
assert on_cifs(target) is expected
```

### Step 5: Call _cifs_table.extend()

```python
_cifs_table.extend(fake_table)
```

### Step 6: Assign unknown = value

```python
_cifs_table[:] = []
```

### Step 7: Call _cifs_table.extend()

```python
_cifs_table.extend(orig_table)
```

**Verification:**
```python
assert on_cifs(target) is False
```


## Complete Example

```python
# Workflow
assert isinstance(_cifs_table, list)
assert isinstance(on_cifs('/'), bool)
fake_table = [('/scratch/tmp', 'ext4'), ('/scratch', 'cifs')]
cifs_targets = [('/scratch/tmp/x/y', False), ('/scratch/tmp/x', False), ('/scratch/x/y', True), ('/scratch/x', True), ('/x/y', False), ('/x', False), ('/', False)]
orig_table = _cifs_table[:]
_cifs_table[:] = []
for target, _ in cifs_targets:
    assert on_cifs(target) is False
_cifs_table.extend(fake_table)
for target, expected in cifs_targets:
    assert on_cifs(target) is expected
_cifs_table[:] = []
_cifs_table.extend(orig_table)
```

## Next Steps


---

*Source: test_filemanip.py:523 | Complexity: Intermediate | Last updated: 2026-05-18*