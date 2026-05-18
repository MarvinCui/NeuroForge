# How To: Convert Noop

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test convert noop

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
# Fixtures: tmp_path
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

### Step 4: Call convert.main()

```python
convert.main([str(infile), str(outfile)])
```

**Verification:**
```python
assert converted.shape == orig.shape
```

### Step 5: Assign converted = nib.load(...)

```python
converted = nib.load(outfile)
```

**Verification:**
```python
assert converted.get_data_dtype() == orig.get_data_dtype()
```

### Step 6: Assign infile = get_test_data(...)

```python
infile = get_test_data(fname='resampled_anat_moved.nii')
```

**Verification:**
```python
assert outfile.is_file()
```

### Step 7: Call convert.main()

```python
convert.main([str(infile), str(outfile), '--force'])
```

**Verification:**
```python
assert not (converted2.shape == converted.shape and np.allclose(converted2.affine, converted.affine) and np.allclose(converted2.get_fdata(), converted.get_fdata()))
```

### Step 8: Assign converted2 = nib.load(...)

```python
converted2 = nib.load(outfile)
```

**Verification:**
```python
assert not (converted2.shape == converted.shape and np.allclose(converted2.affine, converted.affine) and np.allclose(converted2.get_fdata(), converted.get_fdata()))
```

### Step 9: Call convert.main()

```python
convert.main([str(infile), str(outfile)])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
infile = get_test_data(fname='anatomical.nii')
outfile = tmp_path / 'output.nii.gz'
orig = nib.load(infile)
assert not outfile.exists()
convert.main([str(infile), str(outfile)])
assert outfile.is_file()
converted = nib.load(outfile)
assert np.allclose(converted.affine, orig.affine)
assert converted.shape == orig.shape
assert converted.get_data_dtype() == orig.get_data_dtype()
infile = get_test_data(fname='resampled_anat_moved.nii')
with pytest.raises(FileExistsError):
    convert.main([str(infile), str(outfile)])
convert.main([str(infile), str(outfile), '--force'])
assert outfile.is_file()
converted2 = nib.load(outfile)
assert not (converted2.shape == converted.shape and np.allclose(converted2.affine, converted.affine) and np.allclose(converted2.get_fdata(), converted.get_fdata()))
```

## Next Steps


---

*Source: test_convert.py:19 | Complexity: Advanced | Last updated: 2026-05-18*