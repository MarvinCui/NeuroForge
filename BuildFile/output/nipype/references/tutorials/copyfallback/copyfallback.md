# How To: Copyfallback

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test copyfallback

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
assert os.path.exists(tgt_img)
```

### Step 2: Assign unknown = os.path.split(...)

```python
pth, imgname = os.path.split(orig_img)
```

**Verification:**
```python
assert os.path.exists(tgt_hdr)
```

### Step 3: Assign unknown = os.path.split(...)

```python
pth, hdrname = os.path.split(orig_hdr)
```

**Verification:**
```python
assert not os.path.islink(tgt_img)
```

### Step 4: Assign fatfs = TempFATFS(...)

```python
fatfs = TempFATFS()
```

**Verification:**
```python
assert not os.path.islink(tgt_hdr)
```

### Step 5: Assign tgt_img = os.path.join(...)

```python
tgt_img = os.path.join(fatdir, imgname)
```

**Verification:**
```python
assert not os.path.samefile(orig_img, tgt_img)
```

### Step 6: Assign tgt_hdr = os.path.join(...)

```python
tgt_hdr = os.path.join(fatdir, hdrname)
```

**Verification:**
```python
assert not os.path.samefile(orig_hdr, tgt_hdr)
```

### Step 7: Call copyfile()

```python
copyfile(orig_img, tgt_img, copy=copy, use_hardlink=use_hardlink)
```

**Verification:**
```python
assert os.path.exists(tgt_img)
```

### Step 8: Call os.unlink()

```python
os.unlink(tgt_img)
```

### Step 9: Call os.unlink()

```python
os.unlink(tgt_hdr)
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files

# Workflow
if os.name != 'posix':
    return
orig_img, orig_hdr = _temp_analyze_files
pth, imgname = os.path.split(orig_img)
pth, hdrname = os.path.split(orig_hdr)
try:
    fatfs = TempFATFS()
except OSError:
    raise SkipTest('Fuse mount failed. copyfile fallback tests skipped.')
with fatfs as fatdir:
    tgt_img = os.path.join(fatdir, imgname)
    tgt_hdr = os.path.join(fatdir, hdrname)
    for copy in (True, False):
        for use_hardlink in (True, False):
            copyfile(orig_img, tgt_img, copy=copy, use_hardlink=use_hardlink)
            assert os.path.exists(tgt_img)
            assert os.path.exists(tgt_hdr)
            assert not os.path.islink(tgt_img)
            assert not os.path.islink(tgt_hdr)
            assert not os.path.samefile(orig_img, tgt_img)
            assert not os.path.samefile(orig_hdr, tgt_hdr)
            os.unlink(tgt_img)
            os.unlink(tgt_hdr)
```

## Next Steps


---

*Source: test_filemanip.py:231 | Complexity: Advanced | Last updated: 2026-05-18*