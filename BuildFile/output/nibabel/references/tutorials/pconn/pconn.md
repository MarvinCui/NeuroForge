# How To: Pconn

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test pconn

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `nibabel`
- `nibabel.tmpdirs`
- `testing`


## Step-by-Step Guide

### Step 1: Assign mapping = create_parcel_map(...)

```python
mapping = create_parcel_map((0, 1))
```

**Verification:**
```python
assert img.nifti_header.get_intent()[0] == 'ConnParcels'
```

### Step 2: Assign matrix = ci.Cifti2Matrix(...)

```python
matrix = ci.Cifti2Matrix()
```

**Verification:**
```python
assert isinstance(img2, ci.Cifti2Image)
```

### Step 3: Call matrix.append()

```python
matrix.append(mapping)
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), data)
```

### Step 4: Assign hdr = ci.Cifti2Header(...)

```python
hdr = ci.Cifti2Header(matrix)
```

**Verification:**
```python
assert img2.header.matrix.get_index_map(0) == img2.header.matrix.get_index_map(1)
```

### Step 5: Assign data = np.random.randn(...)

```python
data = np.random.randn(4, 4)
```

### Step 6: Assign img = ci.Cifti2Image(...)

```python
img = ci.Cifti2Image(data, hdr)
```

### Step 7: Call img.nifti_header.set_intent()

```python
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_PARCELLATED')
```

### Step 8: Call ci.save()

```python
ci.save(img, 'test.pconn.nii')
```

### Step 9: Assign img2 = ci.load(...)

```python
img2 = ci.load('test.pconn.nii')
```

**Verification:**
```python
assert img.nifti_header.get_intent()[0] == 'ConnParcels'
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

**Verification:**
```python
assert img2.header.matrix.get_index_map(0) == img2.header.matrix.get_index_map(1)
```

### Step 11: Call check_parcel_map()

```python
check_parcel_map(img2.header.matrix.get_index_map(0))
```


## Complete Example

```python
# Workflow
mapping = create_parcel_map((0, 1))
matrix = ci.Cifti2Matrix()
matrix.append(mapping)
hdr = ci.Cifti2Header(matrix)
data = np.random.randn(4, 4)
img = ci.Cifti2Image(data, hdr)
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_PARCELLATED')
with InTemporaryDirectory():
    ci.save(img, 'test.pconn.nii')
    img2 = ci.load('test.pconn.nii')
    assert img.nifti_header.get_intent()[0] == 'ConnParcels'
    assert isinstance(img2, ci.Cifti2Image)
    assert_array_equal(img2.get_fdata(), data)
    assert img2.header.matrix.get_index_map(0) == img2.header.matrix.get_index_map(1)
    check_parcel_map(img2.header.matrix.get_index_map(0))
    del img2
```

## Next Steps


---

*Source: test_new_cifti2.py:487 | Complexity: Advanced | Last updated: 2026-05-18*