# How To: Fetch Files Overwrite

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: Check that fetch_files can overwrite files.

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
# Fixtures: should_cast_path_to_string, tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: 'Check that fetch_files can overwrite files.'

```python
'Check that fetch_files can overwrite files.'
```

**Verification:**
```python
assert request_mocker.url_count == 1
```

### Step 2: Assign files = value

```python
files = ('1.txt', 'http://foo/1.txt')
```

**Verification:**
```python
assert fil.exists()
```

### Step 3: Assign fil = Path(...)

```python
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': True})])[0])
```

**Verification:**
```python
assert not fil.read_text()
```

### Step 4: Call fil.write_text()

```python
fil.write_text('some content')
```

**Verification:**
```python
assert request_mocker.url_count == 1
```

### Step 5: Assign fil = Path(...)

```python
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': False})])[0])
```

**Verification:**
```python
assert fil.exists()
```

### Step 6: Assign fil = Path(...)

```python
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': True})])[0])
```

**Verification:**
```python
assert fil.read_text() == 'some content'
```

### Step 7: Assign tmp_path = str(...)

```python
tmp_path = str(tmp_path)
```

**Verification:**
```python
assert request_mocker.url_count == 2
```


## Complete Example

```python
# Setup
# Fixtures: should_cast_path_to_string, tmp_path, request_mocker

# Workflow
'Check that fetch_files can overwrite files.'
if should_cast_path_to_string:
    tmp_path = str(tmp_path)
files = ('1.txt', 'http://foo/1.txt')
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': True})])[0])
assert request_mocker.url_count == 1
assert fil.exists()
assert not fil.read_text()
fil.write_text('some content')
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': False})])[0])
assert request_mocker.url_count == 1
assert fil.exists()
assert fil.read_text() == 'some content'
fil = Path(_utils.fetch_files(data_dir=tmp_path, verbose=0, files=[(*files, {'overwrite': True})])[0])
assert request_mocker.url_count == 2
assert fil.exists()
assert not fil.read_text()
```

## Next Steps


---

*Source: test_utils.py:583 | Complexity: Intermediate | Last updated: 2026-05-18*