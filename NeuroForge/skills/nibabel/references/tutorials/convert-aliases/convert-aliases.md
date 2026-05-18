# How To: Convert Aliases

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test convert aliases

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.cmdline`
- `nibabel.testing`

**Setup Required:**
```python
# Fixtures: tmp_path, orig_dtype, alias, expected_dtype
```

## Step-by-Step Guide

### Step 1: Assign orig_fname = value

```python
orig_fname = tmp_path / 'orig.nii'
```

**Verification:**
```python
assert orig_fname.exists()
```

### Step 2: Assign out_fname = value

```python
out_fname = tmp_path / 'out.nii'
```

**Verification:**
```python
assert not out_fname.exists()
```

### Step 3: Assign arr = np.arange.reshape(...)

```python
arr = np.arange(24).reshape((2, 3, 4))
```

**Verification:**
```python
assert out_fname.is_file()
```

### Step 4: Assign img = nib.Nifti1Image(...)

```python
img = nib.Nifti1Image(arr, np.eye(4), dtype=orig_dtype)
```

**Verification:**
```python
assert converted.get_data_dtype() == expected_dtype
```

### Step 5: Call img.to_filename()

```python
img.to_filename(orig_fname)
```

**Verification:**
```python
assert orig_fname.exists()
```

### Step 6: Call convert.main()

```python
convert.main([str(orig_fname), str(out_fname), '--out-dtype', alias])
```

**Verification:**
```python
assert out_fname.is_file()
```

### Step 7: Assign expected_dtype = np.dtype.newbyteorder(...)

```python
expected_dtype = np.dtype(expected_dtype).newbyteorder(img.header.endianness)
```

### Step 8: Assign converted = nib.load(...)

```python
converted = nib.load(out_fname)
```

**Verification:**
```python
assert converted.get_data_dtype() == expected_dtype
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, orig_dtype, alias, expected_dtype

# Workflow
orig_fname = tmp_path / 'orig.nii'
out_fname = tmp_path / 'out.nii'
arr = np.arange(24).reshape((2, 3, 4))
img = nib.Nifti1Image(arr, np.eye(4), dtype=orig_dtype)
img.to_filename(orig_fname)
assert orig_fname.exists()
assert not out_fname.exists()
convert.main([str(orig_fname), str(out_fname), '--out-dtype', alias])
assert out_fname.is_file()
expected_dtype = np.dtype(expected_dtype).newbyteorder(img.header.endianness)
converted = nib.load(out_fname)
assert converted.get_data_dtype() == expected_dtype
```

## Next Steps


---

*Source: test_convert.py:153 | Complexity: Advanced | Last updated: 2026-05-18*