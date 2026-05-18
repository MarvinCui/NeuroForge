# How To: Get Dataset Dir Write Access

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check get_dataset_dir can deal with folders with special permissions.

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

### Step 1: 'Check get_dataset_dir can deal with folders with special permissions.'

```python
'Check get_dataset_dir can deal with folders with special permissions.'
```

**Verification:**
```python
assert data_dir == no_write
```

### Step 2: Call os.environ.pop()

```python
os.environ.pop('NILEARN_SHARED_DATA', None)
```

**Verification:**
```python
assert data_dir.exists()
```

### Step 3: Assign no_write = value

```python
no_write = tmp_path / 'no_write'
```

### Step 4: Call no_write.mkdir()

```python
no_write.mkdir(parents=True)
```

### Step 5: Call no_write.chmod()

```python
no_write.chmod(256)
```

### Step 6: Assign expected_base_dir = value

```python
expected_base_dir = tmp_path / 'nilearn_shared_data'
```

### Step 7: Assign unknown = str(...)

```python
os.environ['NILEARN_SHARED_DATA'] = str(expected_base_dir)
```

### Step 8: Assign data_dir = _utils.get_dataset_dir(...)

```python
data_dir = _utils.get_dataset_dir('test', default_paths=[no_write], verbose=0)
```

**Verification:**
```python
assert data_dir == no_write
```

### Step 9: Call no_write.chmod()

```python
no_write.chmod(384)
```

### Step 10: Call shutil.rmtree()

```python
shutil.rmtree(data_dir)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check get_dataset_dir can deal with folders with special permissions.'
os.environ.pop('NILEARN_SHARED_DATA', None)
no_write = tmp_path / 'no_write'
no_write.mkdir(parents=True)
no_write.chmod(256)
expected_base_dir = tmp_path / 'nilearn_shared_data'
os.environ['NILEARN_SHARED_DATA'] = str(expected_base_dir)
data_dir = _utils.get_dataset_dir('test', default_paths=[no_write], verbose=0)
assert data_dir == no_write
assert data_dir.exists()
no_write.chmod(384)
shutil.rmtree(data_dir)
```

## Next Steps


---

*Source: test_utils.py:145 | Complexity: Advanced | Last updated: 2026-05-18*