# How To: Convert Nifti Int Fail

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test convert nifti int fail

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
outfile = tmp_path / 'output.nii'
```

**Verification:**
```python
assert not outfile.exists()
```

### Step 3: Assign orig = nib.load(...)

```python
orig = nib.load(infile)
```

**Verification:**
```python
assert outfile.is_file()
```

### Step 4: Assign converted = nib.load(...)

```python
converted = nib.load(outfile)
```

**Verification:**
```python
assert np.allclose(converted.affine, orig.affine)
```

### Step 5: Call convert.main()

```python
convert.main([str(infile), str(outfile), '--out-dtype', 'int'])
```

**Verification:**
```python
assert converted.shape == orig.shape
```

### Step 6: Call convert.main()

```python
convert.main([str(infile), str(outfile), '--out-dtype', 'int', '--force'])
```

**Verification:**
```python
assert converted.get_data_dtype() == orig.get_data_dtype()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
infile = get_test_data(fname='anatomical.nii')
outfile = tmp_path / 'output.nii'
orig = nib.load(infile)
assert not outfile.exists()
with pytest.raises(ValueError):
    convert.main([str(infile), str(outfile), '--out-dtype', 'int'])
assert not outfile.exists()
with pytest.warns(UserWarning):
    convert.main([str(infile), str(outfile), '--out-dtype', 'int', '--force'])
assert outfile.is_file()
converted = nib.load(outfile)
assert np.allclose(converted.affine, orig.affine)
assert converted.shape == orig.shape
assert converted.get_data_dtype() == orig.get_data_dtype()
```

## Next Steps


---

*Source: test_convert.py:120 | Complexity: Intermediate | Last updated: 2026-05-18*