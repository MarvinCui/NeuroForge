# How To: Convert Imgtype

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test convert imgtype

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
# Fixtures: tmp_path, ext, img_class
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
outfile = tmp_path / f'output.{ext}'
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
convert.main([str(infile), str(outfile), '--image-type', img_class.__name__])
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
assert converted.__class__ == img_class
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, ext, img_class

# Workflow
infile = get_test_data(fname='anatomical.nii')
outfile = tmp_path / f'output.{ext}'
orig = nib.load(infile)
assert not outfile.exists()
convert.main([str(infile), str(outfile), '--image-type', img_class.__name__])
assert outfile.is_file()
converted = nib.load(outfile)
assert np.allclose(converted.affine, orig.affine)
assert converted.shape == orig.shape
assert converted.__class__ == img_class
```

## Next Steps


---

*Source: test_convert.py:104 | Complexity: Intermediate | Last updated: 2026-05-18*