# How To: Spatial Axes First

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test spatial axes first

## Prerequisites

**Required Modules:**
- `os.path`
- `os.path`
- `numpy`
- `nibabel`
- `nibabel.analyze`
- `nibabel.imageclasses`
- `nibabel.nifti1`
- `nibabel.nifti2`
- `nibabel.optpkg`


## Step-by-Step Guide

### Step 1: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

**Verification:**
```python
assert spatial_axes_first(img)
```

### Step 2: Assign img = nib.load(...)

```python
img = nib.load(pjoin(DATA_DIR, fname))
```

**Verification:**
```python
assert len(img.shape) == 3
```

### Step 3: Assign img = nib.load(...)

```python
img = nib.load(pjoin(DATA_DIR, fname))
```

**Verification:**
```python
assert spatial_axes_first(img)
```

### Step 4: Assign data = np.zeros(...)

```python
data = np.zeros(shape)
```

**Verification:**
```python
assert len(img.shape) == 4
```

### Step 5: Assign img = img_class(...)

```python
img = img_class(data, affine)
```

**Verification:**
```python
assert not spatial_axes_first(img)
```


## Complete Example

```python
# Workflow
affine = np.eye(4)
for shape in ((2, 3), (4, 3, 2), (5, 4, 1, 2), (2, 3, 5, 2, 1)):
    for img_class in (AnalyzeImage, Nifti1Image, Nifti2Image):
        data = np.zeros(shape)
        img = img_class(data, affine)
        assert spatial_axes_first(img)
for fname in MINC_3DS:
    img = nib.load(pjoin(DATA_DIR, fname))
    assert len(img.shape) == 3
    assert spatial_axes_first(img)
for fname in MINC_4DS:
    img = nib.load(pjoin(DATA_DIR, fname))
    assert len(img.shape) == 4
    assert not spatial_axes_first(img)
```

## Next Steps


---

*Source: test_imageclasses.py:26 | Complexity: Intermediate | Last updated: 2026-05-18*