# How To: Movetree

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests nilearn.dataset._utils.movetree.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `gzip`
- `os`
- `re`
- `shutil`
- `tarfile`
- `urllib`
- `pathlib`
- `unittest.mock`
- `zipfile`
- `numpy`
- `pytest`
- `requests`
- `nilearn.datasets`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: dir1, dir2
```

## Step-by-Step Guide

### Step 1: 'Tests nilearn.dataset._utils.movetree.'

```python
'Tests nilearn.dataset._utils.movetree.'
```

**Verification:**
```python
assert not d.exists()
```

### Step 2: Assign dir111 = value

```python
dir111 = dir1 / 'dir11'
```

**Verification:**
```python
assert d.exists()
```

### Step 3: Assign dir112 = value

```python
dir112 = dir1 / 'dir12'
```

### Step 4: Assign dir212 = value

```python
dir212 = dir2 / 'dir12'
```

### Step 5: Call dir111.mkdir()

```python
dir111.mkdir()
```

### Step 6: Call dir112.mkdir()

```python
dir112.mkdir()
```

### Step 7: Call dir212.mkdir()

```python
dir212.mkdir()
```

### Step 8: Call unknown.touch()

```python
(dir1 / 'file11').touch()
```

### Step 9: Call unknown.touch()

```python
(dir1 / 'file12').touch()
```

### Step 10: Call unknown.touch()

```python
(dir111 / 'file1111').touch()
```

### Step 11: Call unknown.touch()

```python
(dir112 / 'file1121').touch()
```

### Step 12: Call unknown.touch()

```python
(dir2 / 'file21').touch()
```

### Step 13: Call _utils.movetree()

```python
_utils.movetree(dir1, dir2)
```

### Step 14: Assign dir211 = value

```python
dir211 = dir2 / 'dir11'
```

### Step 15: Assign dir212 = value

```python
dir212 = dir2 / 'dir12'
```

**Verification:**
```python
assert not d.exists()
```


## Complete Example

```python
# Setup
# Fixtures: dir1, dir2

# Workflow
'Tests nilearn.dataset._utils.movetree.'
dir111 = dir1 / 'dir11'
dir112 = dir1 / 'dir12'
dir212 = dir2 / 'dir12'
dir111.mkdir()
dir112.mkdir()
dir212.mkdir()
(dir1 / 'file11').touch()
(dir1 / 'file12').touch()
(dir111 / 'file1111').touch()
(dir112 / 'file1121').touch()
(dir2 / 'file21').touch()
_utils.movetree(dir1, dir2)
for d in [dir111, dir112, dir1 / 'file11', dir1 / 'file12', dir111 / 'file1111', dir112 / 'file1121']:
    assert not d.exists()
dir211 = dir2 / 'dir11'
dir212 = dir2 / 'dir12'
for d in [dir211, dir212, dir2 / 'file21', dir2 / 'file11', dir2 / 'file12', dir211 / 'file1111', dir212 / 'file1121']:
    assert d.exists()
```

## Next Steps


---

*Source: test_utils.py:289 | Complexity: Advanced | Last updated: 2026-05-18*