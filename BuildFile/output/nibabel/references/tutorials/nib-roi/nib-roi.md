# How To: Nib Roi

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nib roi

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `unittest`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.cmdline.roi`
- `nibabel.testing`

**Setup Required:**
```python
# Fixtures: tmp_path, inplace
```

## Step-by-Step Guide

### Step 1: Assign in_file = os.path.join(...)

```python
in_file = os.path.join(data_path, 'functional.nii')
```

**Verification:**
```python
assert retval == 0
```

### Step 2: Assign out_file = str(...)

```python
out_file = str(tmp_path / 'sliced.nii')
```

**Verification:**
```python
assert out_img.shape == in_sliced.shape
```

### Step 3: Assign in_img = nb.load(...)

```python
in_img = nb.load(in_file)
```

**Verification:**
```python
assert np.array_equal(in_data[1:-1, -1:1:-1, :, :5], out_img.dataobj)
```

### Step 4: Assign retval = main(...)

```python
retval = main([in_file, out_file, '-i', '1:-1', '-j', '-1:1:-1', '-k', '::', '-t', ':5'])
```

**Verification:**
```python
assert np.allclose(in_sliced.dataobj, out_img.dataobj)
```

### Step 5: Assign out_img = nb.load(...)

```python
out_img = nb.load(out_file)
```

**Verification:**
```python
assert np.allclose(in_sliced.affine, out_img.affine)
```

### Step 6: Assign in_data = value

```python
in_data = in_img.dataobj[:]
```

### Step 7: Assign in_sliced = value

```python
in_sliced = in_img.slicer[1:-1, -1:1:-1, :, :5]
```

**Verification:**
```python
assert out_img.shape == in_sliced.shape
```

### Step 8: Call in_img.to_filename()

```python
in_img.to_filename(out_file)
```

### Step 9: Assign in_file = out_file

```python
in_file = out_file
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, inplace

# Workflow
in_file = os.path.join(data_path, 'functional.nii')
out_file = str(tmp_path / 'sliced.nii')
in_img = nb.load(in_file)
if inplace:
    in_img.to_filename(out_file)
    in_file = out_file
retval = main([in_file, out_file, '-i', '1:-1', '-j', '-1:1:-1', '-k', '::', '-t', ':5'])
assert retval == 0
out_img = nb.load(out_file)
in_data = in_img.dataobj[:]
in_sliced = in_img.slicer[1:-1, -1:1:-1, :, :5]
assert out_img.shape == in_sliced.shape
assert np.array_equal(in_data[1:-1, -1:1:-1, :, :5], out_img.dataobj)
assert np.allclose(in_sliced.dataobj, out_img.dataobj)
assert np.allclose(in_sliced.affine, out_img.affine)
```

## Next Steps


---

*Source: test_roi.py:106 | Complexity: Advanced | Last updated: 2026-05-18*