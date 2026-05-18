# How To: Dlabel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dlabel

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `nibabel`
- `nibabel.tmpdirs`
- `testing`


## Step-by-Step Guide

### Step 1: Assign label_map = create_label_map(...)

```python
label_map = create_label_map((0,))
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDenseLabel'
```

### Step 2: Assign geometry_map = create_geometry_map(...)

```python
geometry_map = create_geometry_map((1,))
```

**Verification:**
```python
assert isinstance(img2, ci.Cifti2Image)
```

### Step 3: Assign matrix = ci.Cifti2Matrix(...)

```python
matrix = ci.Cifti2Matrix()
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 4: Call matrix.extend()

```python
matrix.extend((label_map, geometry_map))
```

### Step 5: Assign hdr = ci.Cifti2Header(...)

```python
hdr = ci.Cifti2Header(matrix)
```

### Step 6: Assign data = np.random.randn(...)

```python
data = np.random.randn(2, 10)
```

### Step 7: Assign img = ci.Cifti2Image(...)

```python
img = ci.Cifti2Image(data, hdr)
```

### Step 8: Call img.nifti_header.set_intent()

```python
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE_LABELS')
```

### Step 9: Call ci.save()

```python
ci.save(img, 'test.dlabel.nii')
```

### Step 10: Assign img2 = nib.load(...)

```python
img2 = nib.load('test.dlabel.nii')
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDenseLabel'
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 12: Call check_label_map()

```python
check_label_map(img2.header.matrix.get_index_map(0))
```

### Step 13: Call check_geometry_map()

```python
check_geometry_map(img2.header.matrix.get_index_map(1))
```


## Complete Example

```python
# Workflow
label_map = create_label_map((0,))
geometry_map = create_geometry_map((1,))
matrix = ci.Cifti2Matrix()
matrix.extend((label_map, geometry_map))
hdr = ci.Cifti2Header(matrix)
data = np.random.randn(2, 10)
img = ci.Cifti2Image(data, hdr)
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE_LABELS')
with InTemporaryDirectory():
    ci.save(img, 'test.dlabel.nii')
    img2 = nib.load('test.dlabel.nii')
    assert img2.nifti_header.get_intent()[0] == 'ConnDenseLabel'
    assert isinstance(img2, ci.Cifti2Image)
    assert_array_equal(img2.get_fdata(), data)
    check_label_map(img2.header.matrix.get_index_map(0))
    check_geometry_map(img2.header.matrix.get_index_map(1))
    del img2
```

## Next Steps


---

*Source: test_new_cifti2.py:335 | Complexity: Advanced | Last updated: 2026-05-18*