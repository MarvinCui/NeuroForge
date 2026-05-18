# How To: Recopy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test recopy

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
assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
```

### Step 2: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img)
```

**Verification:**
```python
assert hdr_stat == _ignore_atime(os.stat(new_hdr)), err_msg
```

### Step 3: Assign img_link = os.path.join(...)

```python
img_link = os.path.join(pth, 'imglink.img')
```

**Verification:**
```python
assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
```

### Step 4: Assign new_img = os.path.join(...)

```python
new_img = os.path.join(pth, 'newfile.img')
```

**Verification:**
```python
assert hdr_stat == _ignore_atime(os.stat(new_hdr)), err_msg
```

### Step 5: Assign new_hdr = os.path.join(...)

```python
new_hdr = os.path.join(pth, 'newfile.hdr')
```

### Step 6: Call copyfile()

```python
copyfile(orig_img, img_link)
```

### Step 7: Assign kwargs = value

```python
kwargs = {'copy': copy, 'use_hardlink': use_hardlink, 'hashmethod': hashmethod}
```

### Step 8: Call copyfile()

```python
copyfile(orig_img, new_img, **kwargs)
```

### Step 9: Assign img_stat = _ignore_atime(...)

```python
img_stat = _ignore_atime(os.stat(new_img))
```

### Step 10: Assign hdr_stat = _ignore_atime(...)

```python
hdr_stat = _ignore_atime(os.stat(new_hdr))
```

### Step 11: Call copyfile()

```python
copyfile(orig_img, new_img, **kwargs)
```

### Step 12: Assign err_msg = unknown.format(...)

```python
err_msg = 'Regular - OS: {}; Copy: {}; Hardlink: {}'.format(os.name, copy, use_hardlink)
```

**Verification:**
```python
assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
```

### Step 13: Call os.unlink()

```python
os.unlink(new_img)
```

### Step 14: Call os.unlink()

```python
os.unlink(new_hdr)
```

### Step 15: Call copyfile()

```python
copyfile(img_link, new_img, **kwargs)
```

### Step 16: Assign img_stat = _ignore_atime(...)

```python
img_stat = _ignore_atime(os.stat(new_img))
```

### Step 17: Assign hdr_stat = _ignore_atime(...)

```python
hdr_stat = _ignore_atime(os.stat(new_hdr))
```

### Step 18: Call copyfile()

```python
copyfile(img_link, new_img, **kwargs)
```

### Step 19: Assign err_msg = unknown.format(...)

```python
err_msg = 'Symlink - OS: {}; Copy: {}; Hardlink: {}'.format(os.name, copy, use_hardlink)
```

**Verification:**
```python
assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
```

### Step 20: Call os.unlink()

```python
os.unlink(new_img)
```

### Step 21: Call os.unlink()

```python
os.unlink(new_hdr)
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files

# Workflow
orig_img, orig_hdr = _temp_analyze_files
pth, fname = os.path.split(orig_img)
img_link = os.path.join(pth, 'imglink.img')
new_img = os.path.join(pth, 'newfile.img')
new_hdr = os.path.join(pth, 'newfile.hdr')
copyfile(orig_img, img_link)
for copy in (True, False):
    for use_hardlink in (True, False):
        for hashmethod in ('timestamp', 'content'):
            kwargs = {'copy': copy, 'use_hardlink': use_hardlink, 'hashmethod': hashmethod}
            if copy and (not use_hardlink) and (hashmethod == 'timestamp'):
                continue
            copyfile(orig_img, new_img, **kwargs)
            img_stat = _ignore_atime(os.stat(new_img))
            hdr_stat = _ignore_atime(os.stat(new_hdr))
            copyfile(orig_img, new_img, **kwargs)
            err_msg = 'Regular - OS: {}; Copy: {}; Hardlink: {}'.format(os.name, copy, use_hardlink)
            assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
            assert hdr_stat == _ignore_atime(os.stat(new_hdr)), err_msg
            os.unlink(new_img)
            os.unlink(new_hdr)
            copyfile(img_link, new_img, **kwargs)
            img_stat = _ignore_atime(os.stat(new_img))
            hdr_stat = _ignore_atime(os.stat(new_hdr))
            copyfile(img_link, new_img, **kwargs)
            err_msg = 'Symlink - OS: {}; Copy: {}; Hardlink: {}'.format(os.name, copy, use_hardlink)
            assert img_stat == _ignore_atime(os.stat(new_img)), err_msg
            assert hdr_stat == _ignore_atime(os.stat(new_hdr)), err_msg
            os.unlink(new_img)
            os.unlink(new_hdr)
```

## Next Steps


---

*Source: test_filemanip.py:181 | Complexity: Advanced | Last updated: 2026-05-18*