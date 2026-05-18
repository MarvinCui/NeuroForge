# How To: Linkchain

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test linkchain

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
assert os.path.islink(new_img1)
```

### Step 2: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img)
```

**Verification:**
```python
assert os.path.islink(new_hdr1)
```

### Step 3: Assign new_img1 = os.path.join(...)

```python
new_img1 = os.path.join(pth, 'newfile1.img')
```

**Verification:**
```python
assert not os.path.islink(new_img2)
```

### Step 4: Assign new_hdr1 = os.path.join(...)

```python
new_hdr1 = os.path.join(pth, 'newfile1.hdr')
```

**Verification:**
```python
assert not os.path.islink(new_hdr2)
```

### Step 5: Assign new_img2 = os.path.join(...)

```python
new_img2 = os.path.join(pth, 'newfile2.img')
```

**Verification:**
```python
assert not os.path.samefile(orig_img, new_img2)
```

### Step 6: Assign new_hdr2 = os.path.join(...)

```python
new_hdr2 = os.path.join(pth, 'newfile2.hdr')
```

**Verification:**
```python
assert not os.path.samefile(orig_hdr, new_hdr2)
```

### Step 7: Assign new_img3 = os.path.join(...)

```python
new_img3 = os.path.join(pth, 'newfile3.img')
```

**Verification:**
```python
assert not os.path.islink(new_img3)
```

### Step 8: Assign new_hdr3 = os.path.join(...)

```python
new_hdr3 = os.path.join(pth, 'newfile3.hdr')
```

**Verification:**
```python
assert not os.path.islink(new_hdr3)
```

### Step 9: Call copyfile()

```python
copyfile(orig_img, new_img1)
```

**Verification:**
```python
assert os.path.samefile(orig_img, new_img3)
```

### Step 10: Call copyfile()

```python
copyfile(new_img1, new_img2, copy=True)
```

**Verification:**
```python
assert os.path.samefile(orig_hdr, new_hdr3)
```

### Step 11: Call copyfile()

```python
copyfile(new_img1, new_img3, copy=True, use_hardlink=True)
```

**Verification:**
```python
assert not os.path.islink(new_img3)
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files

# Workflow
if os.name != 'posix':
    return
orig_img, orig_hdr = _temp_analyze_files
pth, fname = os.path.split(orig_img)
new_img1 = os.path.join(pth, 'newfile1.img')
new_hdr1 = os.path.join(pth, 'newfile1.hdr')
new_img2 = os.path.join(pth, 'newfile2.img')
new_hdr2 = os.path.join(pth, 'newfile2.hdr')
new_img3 = os.path.join(pth, 'newfile3.img')
new_hdr3 = os.path.join(pth, 'newfile3.hdr')
copyfile(orig_img, new_img1)
assert os.path.islink(new_img1)
assert os.path.islink(new_hdr1)
copyfile(new_img1, new_img2, copy=True)
assert not os.path.islink(new_img2)
assert not os.path.islink(new_hdr2)
assert not os.path.samefile(orig_img, new_img2)
assert not os.path.samefile(orig_hdr, new_hdr2)
copyfile(new_img1, new_img3, copy=True, use_hardlink=True)
assert not os.path.islink(new_img3)
assert not os.path.islink(new_hdr3)
assert os.path.samefile(orig_img, new_img3)
assert os.path.samefile(orig_hdr, new_hdr3)
```

## Next Steps


---

*Source: test_filemanip.py:155 | Complexity: Advanced | Last updated: 2026-05-18*