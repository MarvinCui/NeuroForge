# How To: Mgh Load Fileobj

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mgh load fileobj

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `openers`
- `spatialimages`
- `testing`
- `tests`
- `tests`
- `tmpdirs`
- `volumeutils`
- `wrapstruct`
- `mghformat`


## Step-by-Step Guide

### Step 1: Assign img = MGHImage.load(...)

```python
img = MGHImage.load(MGZ_FNAME)
```

**Verification:**
```python
assert pathlib.Path(img.dataobj.file_like) == pathlib.Path(MGZ_FNAME)
```

### Step 2: Assign bio = io.BytesIO(...)

```python
bio = io.BytesIO(contents)
```

**Verification:**
```python
assert img2.dataobj.file_like is bio
```

### Step 3: Assign fm = MGHImage.make_file_map(...)

```python
fm = MGHImage.make_file_map(mapping=dict(image=bio))
```

**Verification:**
```python
assert_array_equal(img.get_fdata(), img2.get_fdata())
```

### Step 4: Assign img2 = MGHImage.from_file_map(...)

```python
img2 = MGHImage.from_file_map(fm)
```

**Verification:**
```python
assert img2.dataobj.file_like is bio
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(img.get_fdata(), img2.get_fdata())
```

### Step 6: Assign contents = fobj.read(...)

```python
contents = fobj.read()
```


## Complete Example

```python
# Workflow
img = MGHImage.load(MGZ_FNAME)
assert pathlib.Path(img.dataobj.file_like) == pathlib.Path(MGZ_FNAME)
with ImageOpener(MGZ_FNAME) as fobj:
    contents = fobj.read()
bio = io.BytesIO(contents)
fm = MGHImage.make_file_map(mapping=dict(image=bio))
img2 = MGHImage.from_file_map(fm)
assert img2.dataobj.file_like is bio
assert_array_equal(img.get_fdata(), img2.get_fdata())
```

## Next Steps


---

*Source: test_mghformat.py:289 | Complexity: Intermediate | Last updated: 2026-05-18*