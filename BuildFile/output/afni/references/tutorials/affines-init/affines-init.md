# How To: Affines Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test affines init

## Prerequisites

**Required Modules:**
- `__future__`
- `os`
- `py3k`
- `numpy`
- `casting`
- `tmpdirs`
- `spatialimages`
- `affines`
- `nifti1`
- `test_arraywriters`
- `numpy.testing`
- `nose.tools`
- `nose`
- `testing`


## Step-by-Step Guide

### Step 1: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24).reshape((2, 3, 4))
```

**Verification:**
```python
assert_equal(hdr['qform_code'], 0)
```

### Step 2: Assign aff = np.diag(...)

```python
aff = np.diag([2, 3, 4, 1])
```

**Verification:**
```python
assert_equal(hdr['sform_code'], 2)
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

**Verification:**
```python
assert_array_equal(hdr.get_zooms(), [2, 3, 4])
```

### Step 4: Assign hdr = img.get_header(...)

```python
hdr = img.get_header()
```

**Verification:**
```python
assert_array_equal(hdr.get_zooms(), [3, 4, 5])
```

### Step 5: Call assert_equal()

```python
assert_equal(hdr['qform_code'], 0)
```

**Verification:**
```python
assert_equal(new_hdr['qform_code'], 0)
```

### Step 6: Call assert_equal()

```python
assert_equal(hdr['sform_code'], 2)
```

**Verification:**
```python
assert_equal(new_hdr['sform_code'], 2)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(hdr.get_zooms(), [2, 3, 4])
```

**Verification:**
```python
assert_array_equal(new_hdr.get_sform(), aff)
```

### Step 8: Assign qaff = np.diag(...)

```python
qaff = np.diag([3, 4, 5, 1])
```

**Verification:**
```python
assert_array_equal(new_hdr.get_zooms(), [2, 3, 4])
```

### Step 9: Assign saff = np.diag(...)

```python
saff = np.diag([6, 7, 8, 1])
```

**Verification:**
```python
assert_equal(new_hdr['qform_code'], 1)
```

### Step 10: Call hdr.set_qform()

```python
hdr.set_qform(qaff, code='scanner')
```

**Verification:**
```python
assert_array_equal(new_hdr.get_qform(), qaff)
```

### Step 11: Call hdr.set_sform()

```python
hdr.set_sform(saff, code='talairach')
```

**Verification:**
```python
assert_equal(new_hdr['sform_code'], 3)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(hdr.get_zooms(), [3, 4, 5])
```

**Verification:**
```python
assert_array_equal(new_hdr.get_sform(), saff)
```

### Step 13: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff, hdr)
```

**Verification:**
```python
assert_array_equal(new_hdr.get_zooms(), [3, 4, 5])
```

### Step 14: Assign new_hdr = img.get_header(...)

```python
new_hdr = img.get_header()
```

### Step 15: Call assert_equal()

```python
assert_equal(new_hdr['qform_code'], 0)
```

### Step 16: Call assert_equal()

```python
assert_equal(new_hdr['sform_code'], 2)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(new_hdr.get_sform(), aff)
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(new_hdr.get_zooms(), [2, 3, 4])
```

### Step 19: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, None, hdr)
```

### Step 20: Assign new_hdr = img.get_header(...)

```python
new_hdr = img.get_header()
```

### Step 21: Call assert_equal()

```python
assert_equal(new_hdr['qform_code'], 1)
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(new_hdr.get_qform(), qaff)
```

### Step 23: Call assert_equal()

```python
assert_equal(new_hdr['sform_code'], 3)
```

### Step 24: Call assert_array_equal()

```python
assert_array_equal(new_hdr.get_sform(), saff)
```

### Step 25: Call assert_array_equal()

```python
assert_array_equal(new_hdr.get_zooms(), [3, 4, 5])
```


## Complete Example

```python
# Workflow
arr = np.arange(24).reshape((2, 3, 4))
aff = np.diag([2, 3, 4, 1])
img = Nifti1Image(arr, aff)
hdr = img.get_header()
assert_equal(hdr['qform_code'], 0)
assert_equal(hdr['sform_code'], 2)
assert_array_equal(hdr.get_zooms(), [2, 3, 4])
qaff = np.diag([3, 4, 5, 1])
saff = np.diag([6, 7, 8, 1])
hdr.set_qform(qaff, code='scanner')
hdr.set_sform(saff, code='talairach')
assert_array_equal(hdr.get_zooms(), [3, 4, 5])
img = Nifti1Image(arr, aff, hdr)
new_hdr = img.get_header()
assert_equal(new_hdr['qform_code'], 0)
assert_equal(new_hdr['sform_code'], 2)
assert_array_equal(new_hdr.get_sform(), aff)
assert_array_equal(new_hdr.get_zooms(), [2, 3, 4])
img = Nifti1Image(arr, None, hdr)
new_hdr = img.get_header()
assert_equal(new_hdr['qform_code'], 1)
assert_array_equal(new_hdr.get_qform(), qaff)
assert_equal(new_hdr['sform_code'], 3)
assert_array_equal(new_hdr.get_sform(), saff)
assert_array_equal(new_hdr.get_zooms(), [3, 4, 5])
```

## Next Steps


---

*Source: test_nifti1.py:922 | Complexity: Advanced | Last updated: 2026-05-18*