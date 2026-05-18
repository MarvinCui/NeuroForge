# How To: Files Interface

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test files interface

## Prerequisites

**Required Modules:**
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `spatialimages`


## Step-by-Step Guide

### Step 1: Assign arr = np.zeros(...)

```python
arr = np.zeros((2, 3, 4))
```

**Verification:**
```python
assert img.get_filename() == 'test.nii'
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert img.file_map['image'].filename == 'test.nii'
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

**Verification:**
```python
assert img.get_filename() == 'test.img'
```

### Step 4: Call img.set_filename()

```python
img.set_filename('test')
```

**Verification:**
```python
assert img.file_map['image'].filename == 'test.img'
```

### Step 5: Assign img = Nifti1Pair(...)

```python
img = Nifti1Pair(arr, aff)
```

**Verification:**
```python
assert img.file_map['header'].filename == 'test.hdr'
```

### Step 6: Call img.set_filename()

```python
img.set_filename('test')
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), img.get_fdata())
```

### Step 7: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

**Verification:**
```python
assert_array_equal(img2.get_fdata(), img.get_fdata())
```

### Step 8: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['image'].fileobj = BytesIO()
```

### Step 9: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 10: Assign img2 = Nifti1Image.from_file_map(...)

```python
img2 = Nifti1Image.from_file_map(img.file_map)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), img.get_fdata())
```

### Step 12: Assign img = Nifti1Pair(...)

```python
img = Nifti1Pair(arr, aff)
```

### Step 13: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['image'].fileobj = BytesIO()
```

### Step 14: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['header'].fileobj = BytesIO()
```

### Step 15: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 16: Assign img2 = Nifti1Pair.from_file_map(...)

```python
img2 = Nifti1Pair.from_file_map(img.file_map)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(img2.get_fdata(), img.get_fdata())
```

### Step 18: img.file_map['header']

```python
img.file_map['header']
```

### Step 19: Call img.to_file_map()

```python
img.to_file_map()
```


## Complete Example

```python
# Workflow
arr = np.zeros((2, 3, 4))
aff = np.eye(4)
img = Nifti1Image(arr, aff)
img.set_filename('test')
assert img.get_filename() == 'test.nii'
assert img.file_map['image'].filename == 'test.nii'
with pytest.raises(KeyError):
    img.file_map['header']
img = Nifti1Pair(arr, aff)
img.set_filename('test')
assert img.get_filename() == 'test.img'
assert img.file_map['image'].filename == 'test.img'
assert img.file_map['header'].filename == 'test.hdr'
img = Nifti1Image(arr, aff)
img.file_map['image'].fileobj = BytesIO()
img.to_file_map()
img2 = Nifti1Image.from_file_map(img.file_map)
assert_array_equal(img2.get_fdata(), img.get_fdata())
img = Nifti1Pair(arr, aff)
img.file_map['image'].fileobj = BytesIO()
with pytest.raises(FileHolderError):
    img.to_file_map()
img.file_map['header'].fileobj = BytesIO()
img.to_file_map()
img2 = Nifti1Pair.from_file_map(img.file_map)
assert_array_equal(img2.get_fdata(), img.get_fdata())
```

## Next Steps


---

*Source: test_files_interface.py:50 | Complexity: Advanced | Last updated: 2026-05-18*