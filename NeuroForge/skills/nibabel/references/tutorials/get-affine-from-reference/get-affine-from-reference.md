# How To: Get Affine From Reference

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get affine from reference

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel`
- `nibabel.testing`
- `utils`


## Step-by-Step Guide

### Step 1: Assign filename = os.path.join(...)

```python
filename = os.path.join(data_path, 'example_nifti2.nii.gz')
```

**Verification:**
```python
assert_array_equal(get_affine_from_reference(affine), affine)
```

### Step 2: Assign img = nib.load(...)

```python
img = nib.load(filename)
```

**Verification:**
```python
assert_array_equal(get_affine_from_reference(img), affine)
```

### Step 3: Assign affine = value

```python
affine = img.affine
```

**Verification:**
```python
assert_array_equal(get_affine_from_reference(filename), affine)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(get_affine_from_reference(affine), affine)
```

### Step 5: Assign wrong_ref = np.array(...)

```python
wrong_ref = np.array([[1, 2, 3], [4, 5, 6]])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(get_affine_from_reference(img), affine)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(get_affine_from_reference(filename), affine)
```

### Step 8: Call get_affine_from_reference()

```python
get_affine_from_reference(wrong_ref)
```


## Complete Example

```python
# Workflow
filename = os.path.join(data_path, 'example_nifti2.nii.gz')
img = nib.load(filename)
affine = img.affine
assert_array_equal(get_affine_from_reference(affine), affine)
wrong_ref = np.array([[1, 2, 3], [4, 5, 6]])
with pytest.raises(ValueError):
    get_affine_from_reference(wrong_ref)
assert_array_equal(get_affine_from_reference(img), affine)
assert_array_equal(get_affine_from_reference(filename), affine)
```

## Next Steps


---

*Source: test_utils.py:13 | Complexity: Advanced | Last updated: 2026-05-18*