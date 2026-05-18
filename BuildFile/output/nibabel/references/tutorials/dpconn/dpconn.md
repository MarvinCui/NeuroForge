# How To: Dpconn

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dpconn

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `nibabel`
- `nibabel.tmpdirs`
- `testing`


## Step-by-Step Guide

### Step 1: Assign parcel_map = create_parcel_map(...)

```python
parcel_map = create_parcel_map((0,))
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDenseParcel'
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
matrix.extend((parcel_map, geometry_map))
```

### Step 5: Assign hdr = ci.Cifti2Header(...)

```python
hdr = ci.Cifti2Header(matrix)
```

### Step 6: Assign data = np.random.randn(...)

```python
data = np.random.randn(4, 10)
```

### Step 7: Assign img = ci.Cifti2Image(...)

```python
img = ci.Cifti2Image(data, hdr)
```

### Step 8: Call img.nifti_header.set_intent()

```python
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE_PARCELLATED')
```

### Step 9: Call ci.save()

```python
ci.save(img, 'test.dpconn.nii')
```

### Step 10: Assign img2 = ci.load(...)

```python
img2 = ci.load('test.dpconn.nii')
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDenseParcel'
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 12: Call check_parcel_map()

```python
check_parcel_map(img2.header.matrix.get_index_map(0))
```

### Step 13: Call check_geometry_map()

```python
check_geometry_map(img2.header.matrix.get_index_map(1))
```


## Complete Example

```python
# Workflow
parcel_map = create_parcel_map((0,))
geometry_map = create_geometry_map((1,))
matrix = ci.Cifti2Matrix()
matrix.extend((parcel_map, geometry_map))
hdr = ci.Cifti2Header(matrix)
data = np.random.randn(4, 10)
img = ci.Cifti2Image(data, hdr)
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE_PARCELLATED')
with InTemporaryDirectory():
    ci.save(img, 'test.dpconn.nii')
    img2 = ci.load('test.dpconn.nii')
    assert img2.nifti_header.get_intent()[0] == 'ConnDenseParcel'
    assert isinstance(img2, ci.Cifti2Image)
    assert_array_equal(img2.get_fdata(), data)
    check_parcel_map(img2.header.matrix.get_index_map(0))
    check_geometry_map(img2.header.matrix.get_index_map(1))
    del img2
```

## Next Steps


---

*Source: test_new_cifti2.py:444 | Complexity: Advanced | Last updated: 2026-05-18*