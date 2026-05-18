# How To: Orientation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test orientation

## Prerequisites

**Required Modules:**
- `glob`
- `os.path`
- `os.path`
- `warnings`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `fileholders`
- `nifti1`
- `openers`
- `parrec`
- `testing`
- `volumeutils`
- `test_arrayproxy`


## Step-by-Step Guide

### Step 1: Assign hdr = PARRECHeader(...)

```python
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
```

**Verification:**
```python
assert_array_equal(HDR_DEFS['slice orientation'], 1)
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(HDR_DEFS['slice orientation'], 1)
```

**Verification:**
```python
assert hdr.get_slice_orientation() == 'transverse'
```

### Step 3: Assign hdr_defc = value

```python
hdr_defc = hdr.image_defs
```

**Verification:**
```python
assert hdr.get_slice_orientation() == 'sagittal'
```

### Step 4: Assign unknown = 2

```python
hdr_defc['slice orientation'] = 2
```

**Verification:**
```python
assert hdr.get_slice_orientation() == 'coronal'
```

### Step 5: Assign unknown = 3

```python
hdr_defc['slice orientation'] = 3
```

**Verification:**
```python
assert hdr.get_slice_orientation() == 'coronal'
```


## Complete Example

```python
# Workflow
hdr = PARRECHeader(HDR_INFO, HDR_DEFS)
assert_array_equal(HDR_DEFS['slice orientation'], 1)
assert hdr.get_slice_orientation() == 'transverse'
hdr_defc = hdr.image_defs
hdr_defc['slice orientation'] = 2
assert hdr.get_slice_orientation() == 'sagittal'
hdr_defc['slice orientation'] = 3
assert hdr.get_slice_orientation() == 'coronal'
```

## Next Steps


---

*Source: test_parrec.py:248 | Complexity: Intermediate | Last updated: 2026-05-18*