# How To: Nifti Qsform Checks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nifti qsform checks

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

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert fhdr['qform_code'] == 0
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert message == 'qform_code -1 not valid; setting to 0'
```

### Step 3: Assign unknown = value

```python
hdr['qform_code'] = -1
```

**Verification:**
```python
assert fhdr['sform_code'] == 0
```

### Step 4: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 30)
```

**Verification:**
```python
assert message == 'sform_code -1 not valid; setting to 0'
```

### Step 5: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 6: Assign unknown = value

```python
hdr['sform_code'] = -1
```

### Step 7: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 30)
```

**Verification:**
```python
assert fhdr['sform_code'] == 0
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr['qform_code'] = -1
fhdr, message, raiser = self.log_chk(hdr, 30)
assert fhdr['qform_code'] == 0
assert message == 'qform_code -1 not valid; setting to 0'
hdr = HC()
hdr['sform_code'] = -1
fhdr, message, raiser = self.log_chk(hdr, 30)
assert fhdr['sform_code'] == 0
assert message == 'sform_code -1 not valid; setting to 0'
```

## Next Steps


---

*Source: test_nifti1.py:217 | Complexity: Intermediate | Last updated: 2026-05-18*