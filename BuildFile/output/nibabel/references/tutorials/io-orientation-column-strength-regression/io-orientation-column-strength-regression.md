# How To: Io Orientation Column Strength Regression

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test io orientation column strength regression

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `nifti1`
- `orientations`
- `testing`


## Step-by-Step Guide

### Step 1: Assign affine = np.array(...)

```python
affine = np.array([[2.08759499, 0.0770245194, 0.112271041, -16.7531357], [-1.04219818, 0.158019245, -0.0534135476, 12.2405062], [-2.33361936, -0.00166752085, 0.124289364, -10.9963446], [0.0, 0.0, 0.0, 1.0]])
```

**Verification:**
```python
assert_array_equal(iar_ornt, axcodes2ornt('IAR'))
```

### Step 2: Assign iar_ornt = io_orientation(...)

```python
iar_ornt = io_orientation(affine)
```

**Verification:**
```python
assert_array_equal(img_ras_ornt, axcodes2ornt('RAS'))
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(iar_ornt, axcodes2ornt('IAR'))
```

**Verification:**
```python
assert img_ras.shape == (4, 3, 2)
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(np.zeros((2, 3, 4), dtype=np.float32), affine)
```

**Verification:**
```python
assert_array_equal(img_ras_reornt_ornt, axcodes2ornt('RAS'))
```

### Step 5: Assign img_ras = img.as_reoriented(...)

```python
img_ras = img.as_reoriented(iar_ornt)
```

**Verification:**
```python
assert img_ras_reornt.shape == (4, 3, 2)
```

### Step 6: Assign img_ras_ornt = io_orientation(...)

```python
img_ras_ornt = io_orientation(img_ras.affine)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(img_ras_ornt, axcodes2ornt('RAS'))
```

**Verification:**
```python
assert img_ras.shape == (4, 3, 2)
```

### Step 8: Assign img_ras_reornt = img_ras.as_reoriented(...)

```python
img_ras_reornt = img_ras.as_reoriented(img_ras_ornt)
```

### Step 9: Assign img_ras_reornt_ornt = io_orientation(...)

```python
img_ras_reornt_ornt = io_orientation(img_ras_reornt.affine)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(img_ras_reornt_ornt, axcodes2ornt('RAS'))
```

**Verification:**
```python
assert img_ras_reornt.shape == (4, 3, 2)
```


## Complete Example

```python
# Workflow
affine = np.array([[2.08759499, 0.0770245194, 0.112271041, -16.7531357], [-1.04219818, 0.158019245, -0.0534135476, 12.2405062], [-2.33361936, -0.00166752085, 0.124289364, -10.9963446], [0.0, 0.0, 0.0, 1.0]])
iar_ornt = io_orientation(affine)
assert_array_equal(iar_ornt, axcodes2ornt('IAR'))
img = Nifti1Image(np.zeros((2, 3, 4), dtype=np.float32), affine)
img_ras = img.as_reoriented(iar_ornt)
img_ras_ornt = io_orientation(img_ras.affine)
assert_array_equal(img_ras_ornt, axcodes2ornt('RAS'))
assert img_ras.shape == (4, 3, 2)
img_ras_reornt = img_ras.as_reoriented(img_ras_ornt)
img_ras_reornt_ornt = io_orientation(img_ras_reornt.affine)
assert_array_equal(img_ras_reornt_ornt, axcodes2ornt('RAS'))
assert img_ras_reornt.shape == (4, 3, 2)
```

## Next Steps


---

*Source: test_orientations.py:295 | Complexity: Advanced | Last updated: 2026-05-18*