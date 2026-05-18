# How To: Nondefault

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test nondefault

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest`
- `pytest`
- `nibabel`
- `nibabel.cmdline.conform`
- `nibabel.optpkg`
- `nibabel.testing`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign infile = get_test_data(...)

```python
infile = get_test_data(fname='anatomical.nii')
```

**Verification:**
```python
assert outfile.isfile()
```

### Step 2: Assign outfile = value

```python
outfile = tmpdir / 'output.nii.gz'
```

**Verification:**
```python
assert c.shape == out_shape
```

### Step 3: Assign out_shape = value

```python
out_shape = (100, 100, 150)
```

**Verification:**
```python
assert c.header.get_zooms() == voxel_size
```

### Step 4: Assign voxel_size = value

```python
voxel_size = (1, 2, 4)
```

**Verification:**
```python
assert nib.orientations.aff2axcodes(c.affine) == tuple(orientation)
```

### Step 5: Assign orientation = 'LAS'

```python
orientation = 'LAS'
```

### Step 6: Assign args = value

```python
args = f"{infile} {outfile} --out-shape {' '.join(map(str, out_shape))} --voxel-size {' '.join(map(str, voxel_size))} --orientation {orientation}"
```

### Step 7: Call main()

```python
main(args.split())
```

**Verification:**
```python
assert outfile.isfile()
```

### Step 8: Assign c = nib.load(...)

```python
c = nib.load(outfile)
```

**Verification:**
```python
assert c.shape == out_shape
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
infile = get_test_data(fname='anatomical.nii')
outfile = tmpdir / 'output.nii.gz'
out_shape = (100, 100, 150)
voxel_size = (1, 2, 4)
orientation = 'LAS'
args = f"{infile} {outfile} --out-shape {' '.join(map(str, out_shape))} --voxel-size {' '.join(map(str, voxel_size))} --orientation {orientation}"
main(args.split())
assert outfile.isfile()
c = nib.load(outfile)
assert c.shape == out_shape
assert c.header.get_zooms() == voxel_size
assert nib.orientations.aff2axcodes(c.affine) == tuple(orientation)
```

## Next Steps


---

*Source: test_conform.py:43 | Complexity: Advanced | Last updated: 2026-05-18*