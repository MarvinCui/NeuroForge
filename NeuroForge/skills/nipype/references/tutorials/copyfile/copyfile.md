# How To: Copyfile

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test copyfile

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `time`
- `pathlib`
- `unittest`
- `pytest`
- `testing`
- `utils.filemanip`

**Setup Required:**
```python
# Fixtures: _temp_analyze_files
```

## Step-by-Step Guide

### Step 1: Assign unknown = _temp_analyze_files

```python
orig_img, orig_hdr = _temp_analyze_files
```

**Verification:**
```python
assert os.path.exists(new_img)
```

### Step 2: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img)
```

**Verification:**
```python
assert os.path.exists(new_hdr)
```

### Step 3: Assign new_img = os.path.join(...)

```python
new_img = os.path.join(pth, 'newfile.img')
```

### Step 4: Assign new_hdr = os.path.join(...)

```python
new_hdr = os.path.join(pth, 'newfile.hdr')
```

### Step 5: Call copyfile()

```python
copyfile(orig_img, new_img)
```

**Verification:**
```python
assert os.path.exists(new_img)
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files

# Workflow
orig_img, orig_hdr = _temp_analyze_files
pth, fname = os.path.split(orig_img)
new_img = os.path.join(pth, 'newfile.img')
new_hdr = os.path.join(pth, 'newfile.hdr')
copyfile(orig_img, new_img)
assert os.path.exists(new_img)
assert os.path.exists(new_hdr)
```

## Next Steps


---

*Source: test_filemanip.py:118 | Complexity: Intermediate | Last updated: 2026-05-18*