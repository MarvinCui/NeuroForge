# How To: Parse Dataarrays

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test parse dataarrays

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

### Step 1: Assign fn = 'bad_daa.gii'

```python
fn = 'bad_daa.gii'
```

**Verification:**
```python
assert len(w) == 1
```

### Step 2: Assign img = gi.GiftiImage(...)

```python
img = gi.GiftiImage()
```

**Verification:**
```python
assert img.numDA == 0
```

### Step 3: Call save()

```python
save(img, fn)
```

### Step 4: Assign txt = txt.replace(...)

```python
txt = txt.replace('NumberOfDataArrays="0"', 'NumberOfDataArrays ="1"')
```

### Step 5: Assign txt = fp.read(...)

```python
txt = fp.read()
```

### Step 6: Call fp.write()

```python
fp.write(txt)
```

### Step 7: Call warnings.filterwarnings()

```python
warnings.filterwarnings('once', category=UserWarning)
```

### Step 8: Call load()

```python
load(fn)
```

**Verification:**
```python
assert len(w) == 1
```


## Complete Example

```python
# Workflow
fn = 'bad_daa.gii'
img = gi.GiftiImage()
with InTemporaryDirectory():
    save(img, fn)
    with open(fn) as fp:
        txt = fp.read()
    txt = txt.replace('NumberOfDataArrays="0"', 'NumberOfDataArrays ="1"')
    with open(fn, 'w') as fp:
        fp.write(txt)
    with clear_and_catch_warnings() as w:
        warnings.filterwarnings('once', category=UserWarning)
        load(fn)
        assert len(w) == 1
        assert img.numDA == 0
```

## Next Steps


---

*Source: test_parse_gifti_fast.py:387 | Complexity: Advanced | Last updated: 2026-05-18*