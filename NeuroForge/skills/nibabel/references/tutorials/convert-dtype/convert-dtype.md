# How To: Convert Dtype

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test convert dtype

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
# Fixtures: tmp_path, data_dtype
```

## Step-by-Step Guide

### Step 1: Assign infile = get_test_data(...)

```python
infile = get_test_data(fname='anatomical.nii')
```

**Verification:**
```python
assert not outfile.exists()
```

### Step 2: Assign outfile = value

```python
outfile = tmp_path / 'output.nii.gz'
```

**Verification:**
```python
assert outfile.is_file()
```

### Step 3: Assign orig = nib.load(...)

```python
orig = nib.load(infile)
```

**Verification:**
```python
assert np.allclose(converted.affine, orig.affine)
```

### Step 4: Assign expected_dtype = np.dtype.newbyteorder(...)

```python
expected_dtype = np.dtype(data_dtype).newbyteorder(orig.header.endianness)
```

**Verification:**
```python
assert converted.shape == orig.shape
```

### Step 5: Call convert.main()

```python
convert.main([str(infile), str(outfile), '--out-dtype', data_dtype])
```

**Verification:**
```python
assert converted.get_data_dtype() == expected_dtype
```

### Step 6: Assign converted = nib.load(...)

```python
converted = nib.load(outfile)
```

**Verification:**
```python
assert np.allclose(converted.affine, orig.affine)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dtype

# Workflow
infile = get_test_data(fname='anatomical.nii')
outfile = tmp_path / 'output.nii.gz'
orig = nib.load(infile)
assert not outfile.exists()
expected_dtype = np.dtype(data_dtype).newbyteorder(orig.header.endianness)
convert.main([str(infile), str(outfile), '--out-dtype', data_dtype])
assert outfile.is_file()
converted = nib.load(outfile)
assert np.allclose(converted.affine, orig.affine)
assert converted.shape == orig.shape
assert converted.get_data_dtype() == expected_dtype
```

## Next Steps


---

*Source: test_convert.py:52 | Complexity: Intermediate | Last updated: 2026-05-18*