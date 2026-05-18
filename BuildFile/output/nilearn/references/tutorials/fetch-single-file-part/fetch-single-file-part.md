# How To: Fetch Single File Part

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Check that fetch_single_file can fetch part of file.

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
# Fixtures: tmp_path, capsys, request_mocker
```

## Step-by-Step Guide

### Step 1: 'Check that fetch_single_file can fetch part of file.'

```python
'Check that fetch_single_file can fetch part of file.'
```

**Verification:**
```python
assert file_full.exists()
```

### Step 2: Assign url = 'http://foo/temp.txt'

```python
url = 'http://foo/temp.txt'
```

**Verification:**
```python
assert file_full.read_text() == 'Dummy content'
```

### Step 3: Assign file_full = value

```python
file_full = tmp_path / 'temp.txt'
```

**Verification:**
```python
assert 'Resuming failed' not in capsys.readouterr().out
```

### Step 4: Assign file_part = value

```python
file_part = tmp_path / 'temp.txt.part'
```

**Verification:**
```python
assert not file_full.exists()
```

### Step 5: Call file_part.write_text()

```python
file_part.write_text('D')
```

**Verification:**
```python
assert not file_part.exists()
```

### Step 6: Assign unknown = get_response

```python
request_mocker.url_mapping[url] = get_response
```

**Verification:**
```python
assert file_full.exists()
```

### Step 7: Call _utils.fetch_single_file()

```python
_utils.fetch_single_file(url=url, data_dir=tmp_path, resume=True)
```

**Verification:**
```python
assert file_full.read_text() == 'dummy content'
```

### Step 8: Call file_full.unlink()

```python
file_full.unlink()
```

**Verification:**
```python
assert not file_full.exists()
```

### Step 9: Call file_part.write_text()

```python
file_part.write_text('D')
```

### Step 10: Call _utils.fetch_single_file()

```python
_utils.fetch_single_file(url=url, data_dir=tmp_path, resume=True, overwrite=True)
```

**Verification:**
```python
assert file_full.exists()
```

### Step 11: """Create mock Response object with correct content range header."""

```python
"""Create mock Response object with correct content range header."""
```

### Step 12: Assign req_range = request.headers.get(...)

```python
req_range = request.headers.get('Range')
```

### Step 13: Assign resp = Response(...)

```python
resp = Response(b'dummy content', match)
```

### Step 14: Assign resp.iter_start = int(...)

```python
resp.iter_start = int(re.match('bytes=(\\d+)-', req_range)[1])
```

### Step 15: Assign unknown = value

```python
resp.headers['Content-Range'] = f'bytes {resp.iter_start}-{len(resp.content) - 1}/{len(resp.content)}'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, capsys, request_mocker

# Workflow
'Check that fetch_single_file can fetch part of file.'

def get_response(match, request):
    """Create mock Response object with correct content range header."""
    req_range = request.headers.get('Range')
    resp = Response(b'dummy content', match)
    if req_range is not None:
        resp.iter_start = int(re.match('bytes=(\\d+)-', req_range)[1])
        resp.headers['Content-Range'] = f'bytes {resp.iter_start}-{len(resp.content) - 1}/{len(resp.content)}'
    return resp
url = 'http://foo/temp.txt'
file_full = tmp_path / 'temp.txt'
file_part = tmp_path / 'temp.txt.part'
file_part.write_text('D')
request_mocker.url_mapping[url] = get_response
_utils.fetch_single_file(url=url, data_dir=tmp_path, resume=True)
assert file_full.exists()
assert file_full.read_text() == 'Dummy content'
assert 'Resuming failed' not in capsys.readouterr().out
file_full.unlink()
assert not file_full.exists()
assert not file_part.exists()
file_part.write_text('D')
_utils.fetch_single_file(url=url, data_dir=tmp_path, resume=True, overwrite=True)
assert file_full.exists()
assert file_full.read_text() == 'dummy content'
```

## Next Steps


---

*Source: test_utils.py:461 | Complexity: Advanced | Last updated: 2026-05-18*