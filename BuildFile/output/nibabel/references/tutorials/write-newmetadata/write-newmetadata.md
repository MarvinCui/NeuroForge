# How To: Write Newmetadata

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test write newmetadata

## Prerequisites

**Required Modules:**
- `shutil`
- `sys`
- `warnings`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `loadsave`
- `nifti1`
- `testing`
- `tmpdirs`
- `parse_gifti_fast`
- `util`


## Step-by-Step Guide

### Step 1: Assign img = gi.GiftiImage(...)

```python
img = gi.GiftiImage()
```

**Verification:**
```python
assert 'mykey' in myme
```

### Step 2: Assign newmeta = gi.GiftiMetaData(...)

```python
newmeta = gi.GiftiMetaData(mykey='val1')
```

**Verification:**
```python
assert 'mykey1' in myme
```

### Step 3: Assign img.meta = newmeta

```python
img.meta = newmeta
```

**Verification:**
```python
assert 'mykey' not in myme
```

### Step 4: Assign myme = value

```python
myme = img.meta
```

**Verification:**
```python
assert 'mykey' in myme
```

### Step 5: Assign newmeta = gi.GiftiMetaData(...)

```python
newmeta = gi.GiftiMetaData({'mykey1': 'val2'})
```

### Step 6: Assign img.meta = newmeta

```python
img.meta = newmeta
```

### Step 7: Assign myme = value

```python
myme = img.meta
```

**Verification:**
```python
assert 'mykey1' in myme
```


## Complete Example

```python
# Workflow
img = gi.GiftiImage()
newmeta = gi.GiftiMetaData(mykey='val1')
img.meta = newmeta
myme = img.meta
assert 'mykey' in myme
newmeta = gi.GiftiMetaData({'mykey1': 'val2'})
img.meta = newmeta
myme = img.meta
assert 'mykey1' in myme
assert 'mykey' not in myme
```

## Next Steps


---

*Source: test_parse_gifti_fast.py:340 | Complexity: Intermediate | Last updated: 2026-05-18*