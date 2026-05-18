# How To: Lossless Slice Noscaling

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test lossless slice noscaling

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign fname = value

```python
fname = tmp_path / 'image.mgh'
```

**Verification:**
```python
assert np.array_equal(img1.get_fdata()[:, :, 2:4], img2.get_fdata())
```

### Step 2: Assign img = nb.MGHImage(...)

```python
img = nb.MGHImage(np.random.uniform(-20000, 20000, (5, 5, 5, 5)).astype('float32'), affine=np.eye(4))
```

**Verification:**
```python
assert np.array_equal(img1.dataobj.get_unscaled()[:, :, 2:4], img2.dataobj.get_unscaled())
```

### Step 3: Call img.to_filename()

```python
img.to_filename(fname)
```

**Verification:**
```python
assert img1.dataobj.slope == img2.dataobj.slope
```

### Step 4: Assign img1 = nb.load(...)

```python
img1 = nb.load(fname)
```

**Verification:**
```python
assert img1.dataobj.inter == img2.dataobj.inter
```

### Step 5: Assign sliced_fname = value

```python
sliced_fname = tmp_path / 'sliced.mgh'
```

### Step 6: Call lossless_slice.to_filename()

```python
lossless_slice(img1, (slice(None), slice(None), slice(2, 4))).to_filename(sliced_fname)
```

### Step 7: Assign img2 = nb.load(...)

```python
img2 = nb.load(sliced_fname)
```

**Verification:**
```python
assert np.array_equal(img1.get_fdata()[:, :, 2:4], img2.get_fdata())
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
fname = tmp_path / 'image.mgh'
img = nb.MGHImage(np.random.uniform(-20000, 20000, (5, 5, 5, 5)).astype('float32'), affine=np.eye(4))
img.to_filename(fname)
img1 = nb.load(fname)
sliced_fname = tmp_path / 'sliced.mgh'
lossless_slice(img1, (slice(None), slice(None), slice(2, 4))).to_filename(sliced_fname)
img2 = nb.load(sliced_fname)
assert np.array_equal(img1.get_fdata()[:, :, 2:4], img2.get_fdata())
assert np.array_equal(img1.dataobj.get_unscaled()[:, :, 2:4], img2.dataobj.get_unscaled())
assert img1.dataobj.slope == img2.dataobj.slope
assert img1.dataobj.inter == img2.dataobj.inter
```

## Next Steps


---

*Source: test_roi.py:88 | Complexity: Intermediate | Last updated: 2026-05-18*