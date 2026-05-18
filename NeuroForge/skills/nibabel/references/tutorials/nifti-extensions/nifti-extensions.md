# How To: Nifti Extensions

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test nifti extensions

## Prerequisites

**Required Modules:**
- `os`
- `struct`
- `unittest`
- `warnings`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel`
- `nibabel.affines`
- `nibabel.casting`
- `nibabel.eulerangles`
- `nibabel.nifti1`
- `nibabel.optpkg`
- `nibabel.pkg_info`
- `nibabel.spatialimages`
- `nibabel.tmpdirs`
- `freesurfer`
- `orientations`
- `testing`
- `nibabel_data`
- `test_arraywriters`
- `test_orientations`
- `io`
- `json`


## Step-by-Step Guide

### Step 1: Assign nim = load(...)

```python
nim = load(image_file)
```

**Verification:**
```python
assert len(exts_container) == 2
```

### Step 2: Assign hdr = value

```python
hdr = nim.header
```

**Verification:**
```python
assert exts_container.count('comment') == 2
```

### Step 3: Assign exts_container = value

```python
exts_container = hdr.extensions
```

**Verification:**
```python
assert exts_container.count('afni') == 0
```

### Step 4: Assign afniext = Nifti1Extension(...)

```python
afniext = Nifti1Extension('afni', '<xml></xml>')
```

**Verification:**
```python
assert exts_container.get_codes() == [6, 6]
```

### Step 5: Call exts_container.append()

```python
exts_container.append(afniext)
```

**Verification:**
```python
assert exts_container.get_sizeondisk() % 16 == 0
```


## Complete Example

```python
# Workflow
nim = load(image_file)
hdr = nim.header
exts_container = hdr.extensions
assert len(exts_container) == 2
assert exts_container.count('comment') == 2
assert exts_container.count('afni') == 0
assert exts_container.get_codes() == [6, 6]
assert exts_container.get_sizeondisk() % 16 == 0
assert exts_container[0].get_content() == b'extcomment1'
afniext = Nifti1Extension('afni', '<xml></xml>')
exts_container.append(afniext)
assert exts_container.get_codes() == [6, 6, 4]
assert exts_container.count('comment') == 2
assert exts_container.count('afni') == 1
assert exts_container.get_sizeondisk() % 16 == 0
del exts_container[1]
assert exts_container.get_codes() == [6, 4]
assert exts_container.count('comment') == 1
assert exts_container.count('afni') == 1
```

## Next Steps


---

*Source: test_nifti1.py:1348 | Complexity: Intermediate | Last updated: 2026-05-18*