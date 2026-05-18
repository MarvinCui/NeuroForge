# How To: Make Fetcher Http

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test make fetcher http

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
assert (tmp_path / 'sphere_name').is_file()
```

### Step 2: Assign symmetric642 = value

```python
symmetric642 = SPHERE_FILES['symmetric642']
```

**Verification:**
```python
assert not (tmp_path / 'sphere_name2').is_file()
```

### Step 3: Assign stored_md5 = _get_file_md5(...)

```python
stored_md5 = _get_file_md5(symmetric362)
```

**Verification:**
```python
assert _get_file_md5(tmp_path / 'sphere_name') == stored_md5
```

### Step 4: Assign stored_md5_642 = _get_file_md5(...)

```python
stored_md5_642 = _get_file_md5(symmetric642)
```

**Verification:**
```python
assert (tmp_path / 'sphere_name2').is_file()
```

### Step 5: Assign unknown = _free_port_server(...)

```python
server, base_url, original_cwd = _free_port_server(str(Path(symmetric362).parent))
```

**Verification:**
```python
assert _get_file_md5(tmp_path / 'sphere_name2') == stored_md5_642
```

### Step 6: Assign sf = _make_fetcher(...)

```python
sf = _make_fetcher('sphere_fetcher', str(tmp_path), base_url, [Path(symmetric362).name, Path(symmetric642).name], ['sphere_name', 'sphere_name2'], md5_list=[stored_md5, stored_md5_642], optional_fnames=['sphere_name2'])
```

### Step 7: Call sf()

```python
sf()
```

**Verification:**
```python
assert (tmp_path / 'sphere_name').is_file()
```

### Step 8: Call sf()

```python
sf(include_optional=True)
```

**Verification:**
```python
assert (tmp_path / 'sphere_name2').is_file()
```

### Step 9: Call server.shutdown()

```python
server.shutdown()
```

### Step 10: Call os.chdir()

```python
os.chdir(original_cwd)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
symmetric362 = SPHERE_FILES['symmetric362']
symmetric642 = SPHERE_FILES['symmetric642']
stored_md5 = _get_file_md5(symmetric362)
stored_md5_642 = _get_file_md5(symmetric642)
server, base_url, original_cwd = _free_port_server(str(Path(symmetric362).parent))
try:
    sf = _make_fetcher('sphere_fetcher', str(tmp_path), base_url, [Path(symmetric362).name, Path(symmetric642).name], ['sphere_name', 'sphere_name2'], md5_list=[stored_md5, stored_md5_642], optional_fnames=['sphere_name2'])
    sf()
    assert (tmp_path / 'sphere_name').is_file()
    assert not (tmp_path / 'sphere_name2').is_file()
    assert _get_file_md5(tmp_path / 'sphere_name') == stored_md5
    sf(include_optional=True)
    assert (tmp_path / 'sphere_name2').is_file()
    assert _get_file_md5(tmp_path / 'sphere_name2') == stored_md5_642
finally:
    server.shutdown()
    os.chdir(original_cwd)
```

## Next Steps


---

*Source: test_fetcher.py:111 | Complexity: Advanced | Last updated: 2026-05-18*