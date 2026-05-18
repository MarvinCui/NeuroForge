# How To: Handlefilecollision Rename File Exists

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test handleFileCollision rename file exists

## Prerequisites

**Required Modules:**
- `pytest`
- `os`
- `shutil`
- `tempfile`
- `psychopy.tools.fileerrortools`


## Step-by-Step Guide

### Step 1: Assign temp_dir = mkdtemp(...)

```python
temp_dir = mkdtemp()
```

**Verification:**
```python
assert handled_path == expected_path
```

### Step 2: Assign unknown = os.path.splitext(...)

```python
filename, suffix = os.path.splitext(path)
```

### Step 3: Assign expected_path = value

```python
expected_path = '%s_1%s' % (filename, suffix)
```

**Verification:**
```python
assert handled_path == expected_path
```

### Step 4: Call os.rmdir()

```python
os.rmdir(temp_dir)
```

### Step 5: Assign path = value

```python
path = f.name
```

### Step 6: Assign handled_path = handleFileCollision(...)

```python
handled_path = handleFileCollision(fileName=path, fileCollisionMethod='rename')
```


## Complete Example

```python
# Workflow
temp_dir = mkdtemp()
with NamedTemporaryFile(dir=temp_dir, suffix='.xyz') as f:
    path = f.name
    handled_path = handleFileCollision(fileName=path, fileCollisionMethod='rename')
filename, suffix = os.path.splitext(path)
expected_path = '%s_1%s' % (filename, suffix)
assert handled_path == expected_path
os.rmdir(temp_dir)
```

## Next Steps


---

*Source: test_fileerrortools.py:41 | Complexity: Intermediate | Last updated: 2026-05-18*