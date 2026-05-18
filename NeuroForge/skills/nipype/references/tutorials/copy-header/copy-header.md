# How To: Copy Header

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Cover copy_header.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `pytest`
- `imagemanip`

**Setup Required:**
```python
# Fixtures: tmp_path, keep_dtype
```

## Step-by-Step Guide

### Step 1: 'Cover copy_header.'

```python
'Cover copy_header.'
```

**Verification:**
```python
assert np.all(copied.get_qform(coded=False) == ref.get_qform(coded=False))
```

### Step 2: Assign fname1 = value

```python
fname1 = tmp_path / 'reference.nii.gz'
```

**Verification:**
```python
assert np.all(copied.get_sform(coded=False) == ref.get_sform(coded=False))
```

### Step 3: Assign fname2 = value

```python
fname2 = tmp_path / 'target.nii.gz'
```

**Verification:**
```python
assert copied.get_qform(coded=True)[1] == ref.get_qform(coded=True)[1]
```

### Step 4: Assign nii = nb.Nifti1Image(...)

```python
nii = nb.Nifti1Image(np.zeros((10, 10, 10), dtype='uint8'), None, None)
```

**Verification:**
```python
assert copied.get_sform(coded=True)[1] == ref.get_sform(coded=True)[1]
```

### Step 5: Call nii.set_qform()

```python
nii.set_qform(np.diag((1.0, 2.0, 3.0, 1.0)), code=2)
```

**Verification:**
```python
assert (copied.header.get_data_dtype() == ref.header.get_data_dtype()) != keep_dtype
```

### Step 6: Call nii.set_sform()

```python
nii.set_sform(np.diag((1.0, 2.0, 3.0, 1.0)), code=1)
```

### Step 7: Call nii.to_filename()

```python
nii.to_filename(str(fname1))
```

### Step 8: Call nii.set_data_dtype()

```python
nii.set_data_dtype('float32')
```

### Step 9: Call nii.set_qform()

```python
nii.set_qform(np.eye(4), code=1)
```

### Step 10: Call nii.to_filename()

```python
nii.to_filename(str(fname2))
```

### Step 11: Assign copied = nb.load(...)

```python
copied = nb.load(copy_header(fname1, fname2, keep_dtype=keep_dtype))
```

### Step 12: Assign ref = nb.load(...)

```python
ref = nb.load(str(fname1))
```

**Verification:**
```python
assert np.all(copied.get_qform(coded=False) == ref.get_qform(coded=False))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, keep_dtype

# Workflow
'Cover copy_header.'
fname1 = tmp_path / 'reference.nii.gz'
fname2 = tmp_path / 'target.nii.gz'
nii = nb.Nifti1Image(np.zeros((10, 10, 10), dtype='uint8'), None, None)
nii.set_qform(np.diag((1.0, 2.0, 3.0, 1.0)), code=2)
nii.set_sform(np.diag((1.0, 2.0, 3.0, 1.0)), code=1)
nii.to_filename(str(fname1))
nii.set_data_dtype('float32')
nii.set_qform(np.eye(4), code=1)
nii.to_filename(str(fname2))
copied = nb.load(copy_header(fname1, fname2, keep_dtype=keep_dtype))
ref = nb.load(str(fname1))
assert np.all(copied.get_qform(coded=False) == ref.get_qform(coded=False))
assert np.all(copied.get_sform(coded=False) == ref.get_sform(coded=False))
assert copied.get_qform(coded=True)[1] == ref.get_qform(coded=True)[1]
assert copied.get_sform(coded=True)[1] == ref.get_sform(coded=True)[1]
assert (copied.header.get_data_dtype() == ref.header.get_data_dtype()) != keep_dtype
```

## Next Steps


---

*Source: test_imagemanip.py:10 | Complexity: Advanced | Last updated: 2026-05-18*