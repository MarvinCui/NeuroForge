# How To: Nifti Qfac Checks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nifti qfac checks

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

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert fhdr['pixdim'][0] == 1
```

### Step 2: Assign unknown = 1

```python
hdr['pixdim'][0] = 1
```

**Verification:**
```python
assert message == 'pixdim[0] (qfac) should be 1 (default) or -1; setting qfac to 1'
```

### Step 3: Call self.log_chk()

```python
self.log_chk(hdr, 0)
```

### Step 4: Assign unknown = value

```python
hdr['pixdim'][0] = -1
```

### Step 5: Call self.log_chk()

```python
self.log_chk(hdr, 0)
```

### Step 6: Assign unknown = 0

```python
hdr['pixdim'][0] = 0
```

### Step 7: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

**Verification:**
```python
assert fhdr['pixdim'][0] == 1
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
hdr['pixdim'][0] = 1
self.log_chk(hdr, 0)
hdr['pixdim'][0] = -1
self.log_chk(hdr, 0)
hdr['pixdim'][0] = 0
fhdr, message, raiser = self.log_chk(hdr, 20)
assert fhdr['pixdim'][0] == 1
assert message == 'pixdim[0] (qfac) should be 1 (default) or -1; setting qfac to 1'
```

## Next Steps


---

*Source: test_nifti1.py:202 | Complexity: Intermediate | Last updated: 2026-05-18*