# How To: Fetch Data Http

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fetch data http

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign symmetric362 = value

```python
symmetric362 = SPHERE_FILES['symmetric362']
```

**Verification:**
```python
assert newfile.exists()
```

### Step 2: Assign md5 = _get_file_md5(...)

```python
md5 = _get_file_md5(symmetric362)
```

**Verification:**
```python
assert _get_file_md5(newfile) == md5
```

### Step 3: Assign bad_md5 = value

```python
bad_md5 = '8' * len(md5)
```

### Step 4: Assign name = value

```python
name = Path(symmetric362).name
```

### Step 5: Assign newfile = value

```python
newfile = tmp_path / 'testfile.txt'
```

### Step 6: Assign unknown = _free_port_server(...)

```python
server, base_url, original_cwd = _free_port_server(str(Path(symmetric362).parent))
```

### Step 7: Assign url = value

```python
url = base_url + name
```

### Step 8: Call fetch_data()

```python
fetch_data({'testfile.txt': (url, md5)}, str(tmp_path))
```

**Verification:**
```python
assert newfile.exists()
```

### Step 9: Call newfile.write_bytes()

```python
newfile.write_bytes(newfile.read_bytes() + b'junk')
```

### Step 10: Call fetch_data()

```python
fetch_data({'testfile.txt': (url, md5)}, str(tmp_path))
```

**Verification:**
```python
assert _get_file_md5(newfile) == md5
```

### Step 11: Call server.shutdown()

```python
server.shutdown()
```

### Step 12: Call os.chdir()

```python
os.chdir(original_cwd)
```

### Step 13: Call fetch_data()

```python
fetch_data({'testfile.txt': (url, bad_md5)}, str(tmp_path))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
symmetric362 = SPHERE_FILES['symmetric362']
md5 = _get_file_md5(symmetric362)
bad_md5 = '8' * len(md5)
name = Path(symmetric362).name
newfile = tmp_path / 'testfile.txt'
server, base_url, original_cwd = _free_port_server(str(Path(symmetric362).parent))
url = base_url + name
try:
    fetch_data({'testfile.txt': (url, md5)}, str(tmp_path))
    assert newfile.exists()
    newfile.write_bytes(newfile.read_bytes() + b'junk')
    fetch_data({'testfile.txt': (url, md5)}, str(tmp_path))
    assert _get_file_md5(newfile) == md5
    with pytest.raises(FetcherError):
        fetch_data({'testfile.txt': (url, bad_md5)}, str(tmp_path))
finally:
    server.shutdown()
    os.chdir(original_cwd)
```

## Next Steps


---

*Source: test_fetcher.py:142 | Complexity: Advanced | Last updated: 2026-05-18*