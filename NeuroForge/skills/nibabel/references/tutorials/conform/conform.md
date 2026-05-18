# How To: Conform

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test conform

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `warnings`
- `os.path`
- `os.path`
- `numpy`
- `numpy.linalg`
- `nibabel.optpkg`
- `unittest`
- `pytest`
- `numpy.testing`
- `nibabel`
- `nibabel.affines`
- `nibabel.eulerangles`
- `nibabel.nifti1`
- `nibabel.nifti2`
- `nibabel.orientations`
- `nibabel.processing`
- `nibabel.testing`
- `nibabel.tests.test_spaces`
- `test_imageclasses`

**Setup Required:**
```python
# Fixtures: caplog
```

## Step-by-Step Guide

### Step 1: Assign anat = nib.load(...)

```python
anat = nib.load(pjoin(DATA_DIR, 'anatomical.nii'))
```

**Verification:**
```python
assert c.shape == (256, 256, 256)
```

### Step 2: Assign c = conform(...)

```python
c = conform(anat)
```

**Verification:**
```python
assert c.header.get_zooms() == (1, 1, 1)
```

### Step 3: Assign func = nib.load(...)

```python
func = nib.load(pjoin(DATA_DIR, 'functional.nii'))
```

**Verification:**
```python
assert c.dataobj.dtype.type == anat.dataobj.dtype.type
```

### Step 4: Assign c = conform(...)

```python
c = conform(anat, out_shape=(100, 100, 200), voxel_size=(2, 2, 1.5), orientation='LPI', out_class=Nifti2Image)
```

**Verification:**
```python
assert aff2axcodes(c.affine) == ('R', 'A', 'S')
```

### Step 5: Call conform()

```python
conform(func)
```

**Verification:**
```python
assert isinstance(c, Nifti1Image)
```

### Step 6: Call conform()

```python
conform(anat, out_shape=(100, 100))
```

**Verification:**
```python
assert c.shape == (100, 100, 200)
```

### Step 7: Call conform()

```python
conform(anat, voxel_size=(2, 2))
```

**Verification:**
```python
assert c.header.get_zooms() == (2, 2, 1.5)
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
anat = nib.load(pjoin(DATA_DIR, 'anatomical.nii'))
c = conform(anat)
assert c.shape == (256, 256, 256)
assert c.header.get_zooms() == (1, 1, 1)
assert c.dataobj.dtype.type == anat.dataobj.dtype.type
assert aff2axcodes(c.affine) == ('R', 'A', 'S')
assert isinstance(c, Nifti1Image)
with caplog.at_level(logging.CRITICAL):
    c = conform(anat, out_shape=(100, 100, 200), voxel_size=(2, 2, 1.5), orientation='LPI', out_class=Nifti2Image)
assert c.shape == (100, 100, 200)
assert c.header.get_zooms() == (2, 2, 1.5)
assert c.dataobj.dtype.type == anat.dataobj.dtype.type
assert aff2axcodes(c.affine) == ('L', 'P', 'I')
assert isinstance(c, Nifti2Image)
func = nib.load(pjoin(DATA_DIR, 'functional.nii'))
with pytest.raises(ValueError):
    conform(func)
with pytest.raises(ValueError):
    conform(anat, out_shape=(100, 100))
with pytest.raises(ValueError):
    conform(anat, voxel_size=(2, 2))
```

## Next Steps


---

*Source: test_processing.py:465 | Complexity: Intermediate | Last updated: 2026-05-18*