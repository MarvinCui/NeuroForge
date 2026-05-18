# How To: Check Md5 Error Message Contains Checksums

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check md5 error message contains checksums

## Prerequisites

**Required Modules:**
- `http.server`
- `importlib`
- `logging`
- `os`
- `pathlib`
- `shutil`
- `tempfile`
- `threading`
- `pytest`
- `dipy.data`
- `dipy.data.fetcher`
- `dipy.data.fetcher`


## Step-by-Step Guide

### Step 1: Assign unknown = tempfile.mkstemp(...)

```python
fd, fname = tempfile.mkstemp()
```

**Verification:**
```python
assert fname in msg
```

### Step 2: Call os.write()

```python
os.write(fd, b'dipy')
```

**Verification:**
```python
assert stored in msg
```

### Step 3: Call os.close()

```python
os.close(fd)
```

**Verification:**
```python
assert actual in msg
```

### Step 4: Assign actual = _get_file_md5(...)

```python
actual = _get_file_md5(fname)
```

### Step 5: Assign stored = _BAD_MD5

```python
stored = _BAD_MD5
```

### Step 6: Assign msg = str(...)

```python
msg = str(exc_info.value)
```

**Verification:**
```python
assert fname in msg
```

### Step 7: Call os.unlink()

```python
os.unlink(fname)
```

### Step 8: Call check_md5()

```python
check_md5(fname, stored_md5=stored)
```


## Complete Example

```python
# Workflow
fd, fname = tempfile.mkstemp()
os.write(fd, b'dipy')
os.close(fd)
actual = _get_file_md5(fname)
stored = _BAD_MD5
try:
    with pytest.raises(FetcherError) as exc_info:
        check_md5(fname, stored_md5=stored)
    msg = str(exc_info.value)
    assert fname in msg
    assert stored in msg
    assert actual in msg
finally:
    os.unlink(fname)
```

## Next Steps


---

*Source: test_fetcher.py:94 | Complexity: Advanced | Last updated: 2026-05-18*