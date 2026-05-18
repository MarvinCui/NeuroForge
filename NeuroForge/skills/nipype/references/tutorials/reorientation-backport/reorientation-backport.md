# How To: Reorientation Backport

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test reorientation backport

## Prerequisites

**Required Modules:**
- `numpy`
- `nibabel`
- `pytest`
- `looseversion`
- `nibabel.orientations`
- `image`


## Step-by-Step Guide

### Step 1: Assign pixdims = value

```python
pixdims = ((1, 1, 1), (2, 2, 3))
```

**Verification:**
```python
assert img.as_reoriented(identity) is img
```

### Step 2: Assign data = np.random.normal(...)

```python
data = np.random.normal(size=(17, 18, 19, 2))
```

**Verification:**
```python
assert _as_reoriented_backport(img, identity) is img
```

### Step 3: Assign angles = value

```python
angles = np.random.uniform(-np.pi, np.pi, 3) * [1, 0.5, 1]
```

**Verification:**
```python
assert not np.allclose(img.affine, reoriented_a.affine)
```

### Step 4: Assign rot = nb.eulerangles.euler2mat(...)

```python
rot = nb.eulerangles.euler2mat(*angles)
```

**Verification:**
```python
assert not (flips_only and np.allclose(img.get_fdata(), reoriented_a.get_fdata()))
```

### Step 5: Assign scale = np.diag(...)

```python
scale = np.diag(pixdim)
```

**Verification:**
```python
assert flips_only == np.array_equal(img.header.get_dim_info(), reoriented_a.header.get_dim_info())
```

### Step 6: Assign translation = value

```python
translation = np.array((17, 18, 19)) / 2
```

**Verification:**
```python
assert np.allclose(reoriented_a.affine, reoriented_b.affine)
```

### Step 7: Assign affine = nb.affines.from_matvec(...)

```python
affine = nb.affines.from_matvec(rot.dot(scale), translation)
```

**Verification:**
```python
assert np.array_equal(reoriented_a.get_fdata(), reoriented_b.get_fdata())
```

### Step 8: Assign img = nb.Nifti1Image(...)

```python
img = nb.Nifti1Image(data, affine)
```

**Verification:**
```python
assert np.array_equal(reoriented_a.header.get_dim_info(), reoriented_b.header.get_dim_info())
```

### Step 9: Assign dim_info = value

```python
dim_info = {'freq': 0, 'phase': 1, 'slice': 2}
```

### Step 10: Call img.header.set_dim_info()

```python
img.header.set_dim_info(**dim_info)
```

### Step 11: Assign targ_ornt, orig_ornt = nb.io_orientation(...)

```python
targ_ornt = orig_ornt = nb.io_orientation(affine)
```

### Step 12: Assign identity = ornt_transform(...)

```python
identity = ornt_transform(orig_ornt, orig_ornt)
```

### Step 13: Assign transform = ornt_transform(...)

```python
transform = ornt_transform(orig_ornt, targ_ornt)
```

**Verification:**
```python
assert img.as_reoriented(identity) is img
```

### Step 14: Assign reoriented_a = img.as_reoriented(...)

```python
reoriented_a = img.as_reoriented(transform)
```

### Step 15: Assign reoriented_b = _as_reoriented_backport(...)

```python
reoriented_b = _as_reoriented_backport(img, transform)
```

### Step 16: Assign flips_only = value

```python
flips_only = img.shape == reoriented_a.shape
```

**Verification:**
```python
assert not np.allclose(img.affine, reoriented_a.affine)
```

### Step 17: Assign new_code = np.random.choice(...)

```python
new_code = np.random.choice(_orientations)
```

### Step 18: Assign targ_ornt = axcodes2ornt(...)

```python
targ_ornt = axcodes2ornt(new_code)
```


## Complete Example

```python
# Workflow
pixdims = ((1, 1, 1), (2, 2, 3))
data = np.random.normal(size=(17, 18, 19, 2))
for pixdim in pixdims:
    angles = np.random.uniform(-np.pi, np.pi, 3) * [1, 0.5, 1]
    rot = nb.eulerangles.euler2mat(*angles)
    scale = np.diag(pixdim)
    translation = np.array((17, 18, 19)) / 2
    affine = nb.affines.from_matvec(rot.dot(scale), translation)
    img = nb.Nifti1Image(data, affine)
    dim_info = {'freq': 0, 'phase': 1, 'slice': 2}
    img.header.set_dim_info(**dim_info)
    targ_ornt = orig_ornt = nb.io_orientation(affine)
    while np.array_equal(targ_ornt, orig_ornt):
        new_code = np.random.choice(_orientations)
        targ_ornt = axcodes2ornt(new_code)
    identity = ornt_transform(orig_ornt, orig_ornt)
    transform = ornt_transform(orig_ornt, targ_ornt)
    assert img.as_reoriented(identity) is img
    assert _as_reoriented_backport(img, identity) is img
    reoriented_a = img.as_reoriented(transform)
    reoriented_b = _as_reoriented_backport(img, transform)
    flips_only = img.shape == reoriented_a.shape
    assert not np.allclose(img.affine, reoriented_a.affine)
    assert not (flips_only and np.allclose(img.get_fdata(), reoriented_a.get_fdata()))
    assert flips_only == np.array_equal(img.header.get_dim_info(), reoriented_a.header.get_dim_info())
    assert np.allclose(reoriented_a.affine, reoriented_b.affine)
    assert np.array_equal(reoriented_a.get_fdata(), reoriented_b.get_fdata())
    assert np.array_equal(reoriented_a.header.get_dim_info(), reoriented_b.header.get_dim_info())
```

## Next Steps


---

*Source: test_image.py:16 | Complexity: Advanced | Last updated: 2026-05-18*