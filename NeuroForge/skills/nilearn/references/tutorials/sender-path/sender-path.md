# How To: Sender Path

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sender path

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tarfile`
- `zipfile`
- `pathlib`
- `pytest`
- `requests`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn.datasets.tests._testing`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: request_mocker, tmp_path
```

## Step-by-Step Guide

### Step 1: Assign file_path = value

```python
file_path = tmp_path / 'readme.txt'
```

**Verification:**
```python
assert resp.text == str(file_path)
```

### Step 2: Assign unknown = str(...)

```python
request_mocker.url_mapping['*path'] = str(file_path)
```

**Verification:**
```python
assert resp.text == 'hello'
```

### Step 3: Assign unknown = file_path

```python
request_mocker.url_mapping['*content'] = file_path
```

### Step 4: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/path')
```

**Verification:**
```python
assert resp.text == str(file_path)
```

### Step 5: Assign resp = requests.get(...)

```python
resp = requests.get('https://example.org/content')
```

**Verification:**
```python
assert resp.text == 'hello'
```

### Step 6: Call f.write()

```python
f.write('hello')
```


## Complete Example

```python
# Setup
# Fixtures: request_mocker, tmp_path

# Workflow
file_path = tmp_path / 'readme.txt'
with file_path.open('w') as f:
    f.write('hello')
request_mocker.url_mapping['*path'] = str(file_path)
request_mocker.url_mapping['*content'] = file_path
resp = requests.get('https://example.org/path')
assert resp.text == str(file_path)
resp = requests.get('https://example.org/content')
assert resp.text == 'hello'
```

## Next Steps


---

*Source: test_testing.py:162 | Complexity: Intermediate | Last updated: 2026-05-18*