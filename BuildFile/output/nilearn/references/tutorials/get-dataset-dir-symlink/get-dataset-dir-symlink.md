# How To: Get Dataset Dir Symlink

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Make sure get_dataset_dir can handle simlink.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Make sure get_dataset_dir can handle simlink.'

```python
'Make sure get_dataset_dir can handle simlink.'
```

**Verification:**
```python
assert symlink_dir.exists()
```

### Step 2: Assign expected_linked_dir = value

```python
expected_linked_dir = tmp_path / 'linked'
```

**Verification:**
```python
assert data_dir == expected_linked_dir
```

### Step 3: Call expected_linked_dir.mkdir()

```python
expected_linked_dir.mkdir(parents=True)
```

**Verification:**
```python
assert data_dir.exists()
```

### Step 4: Assign expected_base_dir = value

```python
expected_base_dir = tmp_path / 'env_data'
```

### Step 5: Call expected_base_dir.mkdir()

```python
expected_base_dir.mkdir()
```

### Step 6: Assign symlink_dir = value

```python
symlink_dir = expected_base_dir / 'test'
```

### Step 7: Call symlink_dir.symlink_to()

```python
symlink_dir.symlink_to(expected_linked_dir)
```

**Verification:**
```python
assert symlink_dir.exists()
```

### Step 8: Assign data_dir = _utils.get_dataset_dir(...)

```python
data_dir = _utils.get_dataset_dir('test', default_paths=[symlink_dir], verbose=0)
```

**Verification:**
```python
assert data_dir == expected_linked_dir
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Make sure get_dataset_dir can handle simlink.'
expected_linked_dir = tmp_path / 'linked'
expected_linked_dir.mkdir(parents=True)
expected_base_dir = tmp_path / 'env_data'
expected_base_dir.mkdir()
symlink_dir = expected_base_dir / 'test'
symlink_dir.symlink_to(expected_linked_dir)
assert symlink_dir.exists()
data_dir = _utils.get_dataset_dir('test', default_paths=[symlink_dir], verbose=0)
assert data_dir == expected_linked_dir
assert data_dir.exists()
```

## Next Steps


---

*Source: test_utils.py:167 | Complexity: Advanced | Last updated: 2026-05-18*