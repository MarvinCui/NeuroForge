# How To: Legacy Underscore Content

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: Verify that subclasses that depended on access to ._content continue to work.

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

### Step 1: 'Verify that subclasses that depended on access to ._content continue to work.'

```python
'Verify that subclasses that depended on access to ._content continue to work.'
```

**Verification:**
```python
assert isinstance(ext._content, dict)
```

### Step 2: Assign ext = MyLegacyExtension(...)

```python
ext = MyLegacyExtension(0, '{}')
```

**Verification:**
```python
assert ext._content is ext._content
```

### Step 3: Assign unknown = 1

```python
ext._content['val'] = 1
```

**Verification:**
```python
assert fobj.getvalue() == b' \x00\x00\x00\x00\x00\x00\x00{"val": 1}' + bytes(14)
```

### Step 4: Assign fobj = io.BytesIO(...)

```python
fobj = io.BytesIO()
```

### Step 5: Call ext.write_to()

```python
ext.write_to(fobj)
```

**Verification:**
```python
assert fobj.getvalue() == b' \x00\x00\x00\x00\x00\x00\x00{"val": 1}' + bytes(14)
```

### Step 6: Assign value = value.decode(...)

```python
value = value.decode()
```


## Complete Example

```python
# Workflow
'Verify that subclasses that depended on access to ._content continue to work.'
import io
import json

class MyLegacyExtension(Nifti1Extension):

    def _mangle(self, value):
        return json.dumps(value).encode()

    def _unmangle(self, value):
        if isinstance(value, bytes):
            value = value.decode()
        return json.loads(value)
ext = MyLegacyExtension(0, '{}')
assert isinstance(ext._content, dict)
assert ext._content is ext._content
ext._content['val'] = 1
fobj = io.BytesIO()
ext.write_to(fobj)
assert fobj.getvalue() == b' \x00\x00\x00\x00\x00\x00\x00{"val": 1}' + bytes(14)
```

## Next Steps


---

*Source: test_nifti1.py:1259 | Complexity: Intermediate | Last updated: 2026-05-18*