# How To: Dconn

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dconn

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `nibabel`
- `nibabel.tmpdirs`
- `testing`


## Step-by-Step Guide

### Step 1: Assign mapping = create_geometry_map(...)

```python
mapping = create_geometry_map((0, 1))
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDense'
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
data = np.random.randn(10, 10)
```

### Step 6: Assign img = ci.Cifti2Image(...)

```python
img = ci.Cifti2Image(data, hdr)
```

### Step 7: Call img.nifti_header.set_intent()

```python
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE')
```

### Step 8: Call ci.save()

```python
ci.save(img, 'test.dconn.nii')
```

### Step 9: Assign img2 = nib.load(...)

```python
img2 = nib.load('test.dconn.nii')
```

**Verification:**
```python
assert img2.nifti_header.get_intent()[0] == 'ConnDense'
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), data)
```

**Verification:**
```python
assert img2.header.matrix.get_index_map(0) == img2.header.matrix.get_index_map(1)
```

### Step 11: Call check_geometry_map()

```python
check_geometry_map(img2.header.matrix.get_index_map(0))
```


## Complete Example

```python
# Workflow
mapping = create_geometry_map((0, 1))
matrix = ci.Cifti2Matrix()
matrix.append(mapping)
hdr = ci.Cifti2Header(matrix)
data = np.random.randn(10, 10)
img = ci.Cifti2Image(data, hdr)
img.nifti_header.set_intent('NIFTI_INTENT_CONNECTIVITY_DENSE')
with InTemporaryDirectory():
    ci.save(img, 'test.dconn.nii')
    img2 = nib.load('test.dconn.nii')
    assert img2.nifti_header.get_intent()[0] == 'ConnDense'
    assert isinstance(img2, ci.Cifti2Image)
    assert_array_equal(img2.get_fdata(), data)
    assert img2.header.matrix.get_index_map(0) == img2.header.matrix.get_index_map(1)
    check_geometry_map(img2.header.matrix.get_index_map(0))
    del img2
```

## Next Steps


---

*Source: test_new_cifti2.py:357 | Complexity: Advanced | Last updated: 2026-05-18*