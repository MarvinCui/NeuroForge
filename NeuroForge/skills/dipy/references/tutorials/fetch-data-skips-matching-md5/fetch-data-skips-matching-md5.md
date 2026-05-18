# How To: Fetch Data Skips Matching Md5

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fetch data skips matching md5

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
# Fixtures: tmp_path, sphere_server
```

## Step-by-Step Guide

### Step 1: Assign unknown = sphere_server

```python
base_url, name, md5 = sphere_server
```

**Verification:**
```python
assert dst.stat().st_mtime_ns == mtime_before
```

### Step 2: Assign src = value

```python
src = SPHERE_FILES['symmetric362']
```

### Step 3: Assign dst = value

```python
dst = tmp_path / name
```

### Step 4: Call shutil.copy()

```python
shutil.copy(src, dst)
```

### Step 5: Assign mtime_before = value

```python
mtime_before = dst.stat().st_mtime_ns
```

### Step 6: Call fetch_data()

```python
fetch_data({name: (base_url + name, md5)}, str(tmp_path))
```

**Verification:**
```python
assert dst.stat().st_mtime_ns == mtime_before
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, sphere_server

# Workflow
base_url, name, md5 = sphere_server
src = SPHERE_FILES['symmetric362']
dst = tmp_path / name
shutil.copy(src, dst)
mtime_before = dst.stat().st_mtime_ns
fetch_data({name: (base_url + name, md5)}, str(tmp_path))
assert dst.stat().st_mtime_ns == mtime_before
```

## Next Steps


---

*Source: test_fetcher.py:180 | Complexity: Intermediate | Last updated: 2026-05-18*