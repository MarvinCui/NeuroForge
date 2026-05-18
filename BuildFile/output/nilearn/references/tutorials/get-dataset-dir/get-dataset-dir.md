# How To: Get Dataset Dir

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test folder creation under different environments.

Enforcing a custom clean install.

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

### Step 1: 'Test folder creation under different environments.\n\n    Enforcing a custom clean install.\n    '

```python
'Test folder creation under different environments.\n\n    Enforcing a custom clean install.\n    '
```

**Verification:**
```python
assert data_dir == expected_base_dir / 'test'
```

### Step 2: Call os.environ.pop()

```python
os.environ.pop('NILEARN_DATA', None)
```

**Verification:**
```python
assert data_dir.exists()
```

### Step 3: Call os.environ.pop()

```python
os.environ.pop('NILEARN_SHARED_DATA', None)
```

**Verification:**
```python
assert data_dir == expected_base_dir / 'test'
```

### Step 4: Assign expected_base_dir = Path.expanduser(...)

```python
expected_base_dir = Path('~/nilearn_data').expanduser()
```

**Verification:**
```python
assert data_dir.exists()
```

### Step 5: Assign data_dir = _utils.get_dataset_dir(...)

```python
data_dir = _utils.get_dataset_dir('test', verbose=0)
```

**Verification:**
```python
assert data_dir == expected_base_dir / 'test'
```

### Step 6: Call shutil.rmtree()

```python
shutil.rmtree(data_dir)
```

**Verification:**
```python
assert data_dir.exists()
```

### Step 7: Assign expected_base_dir = value

```python
expected_base_dir = tmp_path / 'test_nilearn_data'
```

### Step 8: Assign unknown = str(...)

```python
os.environ['NILEARN_DATA'] = str(expected_base_dir)
```

### Step 9: Assign data_dir = _utils.get_dataset_dir(...)

```python
data_dir = _utils.get_dataset_dir('test', verbose=0)
```

**Verification:**
```python
assert data_dir == expected_base_dir / 'test'
```

### Step 10: Call shutil.rmtree()

```python
shutil.rmtree(data_dir)
```

### Step 11: Assign expected_base_dir = value

```python
expected_base_dir = tmp_path / 'nilearn_shared_data'
```

### Step 12: Assign unknown = str(...)

```python
os.environ['NILEARN_SHARED_DATA'] = str(expected_base_dir)
```

### Step 13: Assign data_dir = _utils.get_dataset_dir(...)

```python
data_dir = _utils.get_dataset_dir('test', verbose=0)
```

**Verification:**
```python
assert data_dir == expected_base_dir / 'test'
```

### Step 14: Call shutil.rmtree()

```python
shutil.rmtree(data_dir)
```

### Step 15: Assign test_file = value

```python
test_file = tmp_path / 'some_file'
```

### Step 16: Call test_file.write_text()

```python
test_file.write_text('abcfeg')
```

### Step 17: Call _utils.get_dataset_dir()

```python
_utils.get_dataset_dir('test', test_file, verbose=0)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test folder creation under different environments.\n\n    Enforcing a custom clean install.\n    '
os.environ.pop('NILEARN_DATA', None)
os.environ.pop('NILEARN_SHARED_DATA', None)
expected_base_dir = Path('~/nilearn_data').expanduser()
data_dir = _utils.get_dataset_dir('test', verbose=0)
assert data_dir == expected_base_dir / 'test'
assert data_dir.exists()
shutil.rmtree(data_dir)
expected_base_dir = tmp_path / 'test_nilearn_data'
os.environ['NILEARN_DATA'] = str(expected_base_dir)
data_dir = _utils.get_dataset_dir('test', verbose=0)
assert data_dir == expected_base_dir / 'test'
assert data_dir.exists()
shutil.rmtree(data_dir)
expected_base_dir = tmp_path / 'nilearn_shared_data'
os.environ['NILEARN_SHARED_DATA'] = str(expected_base_dir)
data_dir = _utils.get_dataset_dir('test', verbose=0)
assert data_dir == expected_base_dir / 'test'
assert data_dir.exists()
shutil.rmtree(data_dir)
test_file = tmp_path / 'some_file'
test_file.write_text('abcfeg')
with pytest.raises(OSError, match='Nilearn tried to store the dataset in the following directories, but'):
    _utils.get_dataset_dir('test', test_file, verbose=0)
```

## Next Steps


---

*Source: test_utils.py:76 | Complexity: Advanced | Last updated: 2026-05-18*