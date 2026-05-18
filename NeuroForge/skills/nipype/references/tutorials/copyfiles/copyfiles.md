# How To: Copyfiles

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test copyfiles

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
# Fixtures: _temp_analyze_files, _temp_analyze_files_prime
```

## Step-by-Step Guide

### Step 1: Assign unknown = _temp_analyze_files

```python
orig_img1, orig_hdr1 = _temp_analyze_files
```

**Verification:**
```python
assert os.path.exists(new_img1)
```

### Step 2: Assign unknown = _temp_analyze_files_prime

```python
orig_img2, orig_hdr2 = _temp_analyze_files_prime
```

**Verification:**
```python
assert os.path.exists(new_hdr1)
```

### Step 3: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img1)
```

**Verification:**
```python
assert os.path.exists(new_img2)
```

### Step 4: Assign new_img1 = os.path.join(...)

```python
new_img1 = os.path.join(pth, 'newfile.img')
```

**Verification:**
```python
assert os.path.exists(new_hdr2)
```

### Step 5: Assign new_hdr1 = os.path.join(...)

```python
new_hdr1 = os.path.join(pth, 'newfile.hdr')
```

### Step 6: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img2)
```

### Step 7: Assign new_img2 = os.path.join(...)

```python
new_img2 = os.path.join(pth, 'secondfile.img')
```

### Step 8: Assign new_hdr2 = os.path.join(...)

```python
new_hdr2 = os.path.join(pth, 'secondfile.hdr')
```

### Step 9: Call copyfiles()

```python
copyfiles([orig_img1, orig_img2], [new_img1, new_img2])
```

**Verification:**
```python
assert os.path.exists(new_img1)
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files, _temp_analyze_files_prime

# Workflow
orig_img1, orig_hdr1 = _temp_analyze_files
orig_img2, orig_hdr2 = _temp_analyze_files_prime
pth, fname = os.path.split(orig_img1)
new_img1 = os.path.join(pth, 'newfile.img')
new_hdr1 = os.path.join(pth, 'newfile.hdr')
pth, fname = os.path.split(orig_img2)
new_img2 = os.path.join(pth, 'secondfile.img')
new_hdr2 = os.path.join(pth, 'secondfile.hdr')
copyfiles([orig_img1, orig_img2], [new_img1, new_img2])
assert os.path.exists(new_img1)
assert os.path.exists(new_hdr1)
assert os.path.exists(new_img2)
assert os.path.exists(new_hdr2)
```

## Next Steps


---

*Source: test_filemanip.py:139 | Complexity: Advanced | Last updated: 2026-05-18*