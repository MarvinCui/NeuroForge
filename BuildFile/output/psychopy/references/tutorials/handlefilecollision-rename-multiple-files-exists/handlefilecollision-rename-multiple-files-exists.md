# How To: Handlefilecollision Rename Multiple Files Exists

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test handleFileCollision rename multiple files exists

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

### Step 2: Assign path = os.path.join(...)

```python
path = os.path.join(temp_dir, 'test.txt')
```

### Step 3: Assign unknown = os.path.splitext(...)

```python
filename, suffix = os.path.splitext(path)
```

### Step 4: Call shutil.rmtree()

```python
shutil.rmtree(temp_dir)
```

### Step 5: Call f.write()

```python
f.write('foo')
```

### Step 6: Assign handled_path = handleFileCollision(...)

```python
handled_path = handleFileCollision(fileName=path, fileCollisionMethod='rename')
```

### Step 7: Assign expected_path = value

```python
expected_path = '%s_%i%s' % (filename, i, suffix)
```

**Verification:**
```python
assert handled_path == expected_path
```

### Step 8: Call f.write()

```python
f.write('foo')
```


## Complete Example

```python
# Workflow
temp_dir = mkdtemp()
path = os.path.join(temp_dir, 'test.txt')
filename, suffix = os.path.splitext(path)
with open(path, 'w') as f:
    f.write('foo')
for i, _ in enumerate(range(10), start=1):
    handled_path = handleFileCollision(fileName=path, fileCollisionMethod='rename')
    expected_path = '%s_%i%s' % (filename, i, suffix)
    assert handled_path == expected_path
    with open(handled_path, 'w') as f:
        f.write('foo')
shutil.rmtree(temp_dir)
```

## Next Steps


---

*Source: test_fileerrortools.py:58 | Complexity: Advanced | Last updated: 2026-05-18*