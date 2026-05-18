# How To: Files Interface

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test files interface

## Prerequisites

**Required Modules:**
- `numpy`
- `py3k`
- `fileholders`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign arr = np.zeros(...)

```python
arr = np.zeros((2, 3, 4))
```

**Verification:**
```python
assert_equal(img.get_filename(), 'test.nii')
```

### Step 2: Assign aff = np.eye(...)

```python
aff = np.eye(4)
```

**Verification:**
```python
assert_equal(img.file_map['image'].filename, 'test.nii')
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

**Verification:**
```python
assert_raises(KeyError, img.file_map.__getitem__, 'header')
```

### Step 4: Call img.set_filename()

```python
img.set_filename('test')
```

**Verification:**
```python
assert_equal(img.get_filename(), 'test.img')
```

### Step 5: Call assert_equal()

```python
assert_equal(img.get_filename(), 'test.nii')
```

**Verification:**
```python
assert_equal(img.file_map['image'].filename, 'test.img')
```

### Step 6: Call assert_equal()

```python
assert_equal(img.file_map['image'].filename, 'test.nii')
```

**Verification:**
```python
assert_equal(img.file_map['header'].filename, 'test.hdr')
```

### Step 7: Call assert_raises()

```python
assert_raises(KeyError, img.file_map.__getitem__, 'header')
```

**Verification:**
```python
assert_array_equal(img2.get_data(), img.get_data())
```

### Step 8: Assign img = Nifti1Pair(...)

```python
img = Nifti1Pair(arr, aff)
```

**Verification:**
```python
assert_raises(FileHolderError, img.to_file_map)
```

### Step 9: Call img.set_filename()

```python
img.set_filename('test')
```

**Verification:**
```python
assert_array_equal(img2.get_data(), img.get_data())
```

### Step 10: Call assert_equal()

```python
assert_equal(img.get_filename(), 'test.img')
```

### Step 11: Call assert_equal()

```python
assert_equal(img.file_map['image'].filename, 'test.img')
```

### Step 12: Call assert_equal()

```python
assert_equal(img.file_map['header'].filename, 'test.hdr')
```

### Step 13: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(arr, aff)
```

### Step 14: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['image'].fileobj = BytesIO()
```

### Step 15: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 16: Assign img2 = Nifti1Image.from_file_map(...)

```python
img2 = Nifti1Image.from_file_map(img.file_map)
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(img2.get_data(), img.get_data())
```

### Step 18: Assign img = Nifti1Pair(...)

```python
img = Nifti1Pair(arr, aff)
```

### Step 19: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['image'].fileobj = BytesIO()
```

### Step 20: Call assert_raises()

```python
assert_raises(FileHolderError, img.to_file_map)
```

### Step 21: Assign unknown.fileobj = BytesIO(...)

```python
img.file_map['header'].fileobj = BytesIO()
```

### Step 22: Call img.to_file_map()

```python
img.to_file_map()
```

### Step 23: Assign img2 = Nifti1Pair.from_file_map(...)

```python
img2 = Nifti1Pair.from_file_map(img.file_map)
```

### Step 24: Call assert_array_equal()

```python
assert_array_equal(img2.get_data(), img.get_data())
```


## Complete Example

```python
# Workflow
arr = np.zeros((2, 3, 4))
aff = np.eye(4)
img = Nifti1Image(arr, aff)
img.set_filename('test')
assert_equal(img.get_filename(), 'test.nii')
assert_equal(img.file_map['image'].filename, 'test.nii')
assert_raises(KeyError, img.file_map.__getitem__, 'header')
img = Nifti1Pair(arr, aff)
img.set_filename('test')
assert_equal(img.get_filename(), 'test.img')
assert_equal(img.file_map['image'].filename, 'test.img')
assert_equal(img.file_map['header'].filename, 'test.hdr')
img = Nifti1Image(arr, aff)
img.file_map['image'].fileobj = BytesIO()
img.to_file_map()
img2 = Nifti1Image.from_file_map(img.file_map)
assert_array_equal(img2.get_data(), img.get_data())
img = Nifti1Pair(arr, aff)
img.file_map['image'].fileobj = BytesIO()
assert_raises(FileHolderError, img.to_file_map)
img.file_map['header'].fileobj = BytesIO()
img.to_file_map()
img2 = Nifti1Pair.from_file_map(img.file_map)
assert_array_equal(img2.get_data(), img.get_data())
```

## Next Steps


---

*Source: test_files_interface.py:47 | Complexity: Advanced | Last updated: 2026-05-18*