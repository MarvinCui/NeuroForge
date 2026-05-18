# How To: Extension Content Access

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test extension content access

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

### Step 1: Assign ext = Nifti1Extension(...)

```python
ext = Nifti1Extension('comment', b'123')
```

**Verification:**
```python
assert ext.get_content() == b'123'
```

### Step 2: Assign ext.encoding = 'ascii'

```python
ext.encoding = 'ascii'
```

**Verification:**
```python
assert ext.content == b'123'
```

### Step 3: Assign ascii_ext = Nifti1Extension(...)

```python
ascii_ext = Nifti1Extension('comment', 'hôpital'.encode())
```

**Verification:**
```python
assert ext.text == '123'
```

### Step 4: Assign ascii_ext.encoding = 'ascii'

```python
ascii_ext.encoding = 'ascii'
```

**Verification:**
```python
assert ext.json() == 123
```

### Step 5: Assign json_ext = Nifti1Extension(...)

```python
json_ext = Nifti1Extension('unknown', b'{"a": 1}')
```

**Verification:**
```python
assert ext.text == '123'
```

### Step 6: ascii_ext.text

```python
ascii_ext.text
```

**Verification:**
```python
assert json_ext.content == b'{"a": 1}'
```


## Complete Example

```python
# Workflow
ext = Nifti1Extension('comment', b'123')
assert ext.get_content() == b'123'
assert ext.content == b'123'
assert ext.text == '123'
assert ext.json() == 123
ext.encoding = 'ascii'
assert ext.text == '123'
ascii_ext = Nifti1Extension('comment', 'hôpital'.encode())
ascii_ext.encoding = 'ascii'
with pytest.raises(UnicodeDecodeError):
    ascii_ext.text
json_ext = Nifti1Extension('unknown', b'{"a": 1}')
assert json_ext.content == b'{"a": 1}'
assert json_ext.text == '{"a": 1}'
assert json_ext.json() == {'a': 1}
```

## Next Steps


---

*Source: test_nifti1.py:1233 | Complexity: Intermediate | Last updated: 2026-05-18*