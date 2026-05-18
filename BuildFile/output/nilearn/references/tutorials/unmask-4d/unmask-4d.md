# How To: Unmask 4D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test unmask on 4D images.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.preprocessing`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.masking`
- `nilearn.surface.surface`

**Setup Required:**
```python
# Fixtures: rng, affine_eye, shape_4d_default
```

## Step-by-Step Guide

### Step 1: 'Test unmask on 4D images.'

```python
'Test unmask on 4D images.'
```

**Verification:**
```python
assert t.ndim == 4
```

### Step 2: Assign data4D = rng.uniform(...)

```python
data4D = rng.uniform(size=shape_4d_default)
```

**Verification:**
```python
assert t.flags['C_CONTIGUOUS']
```

### Step 3: Assign mask = rng.integers(...)

```python
mask = rng.integers(2, size=shape_4d_default[:3], dtype='int32')
```

**Verification:**
```python
assert not t.flags['F_CONTIGUOUS']
```

### Step 4: Assign mask_img = Nifti1Image(...)

```python
mask_img = Nifti1Image(mask, affine_eye)
```

**Verification:**
```python
assert_array_equal(t, unmasked4D)
```

### Step 5: Assign mask = mask.astype(...)

```python
mask = mask.astype(bool)
```

**Verification:**
```python
assert isinstance(t, list)
```

### Step 6: Assign masked4D = value

```python
masked4D = data4D[mask, :].T
```

**Verification:**
```python
assert t[0].ndim == 4
```

### Step 7: Assign unmasked4D = data4D.copy(...)

```python
unmasked4D = data4D.copy()
```

**Verification:**
```python
assert not t[0].flags['C_CONTIGUOUS']
```

### Step 8: Assign unknown = 0

```python
unmasked4D[np.logical_not(mask), :] = 0
```

**Verification:**
```python
assert t[0].flags['F_CONTIGUOUS']
```

### Step 9: Assign t = get_data(...)

```python
t = get_data(unmask(masked4D, mask_img, order='C'))
```

**Verification:**
```python
assert_array_equal(t[0], unmasked4D)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(t, unmasked4D)
```

### Step 11: Assign t = unmask(...)

```python
t = unmask([masked4D], mask_img, order='F')
```

### Step 12: Assign t = value

```python
t = [get_data(t_) for t_ in t]
```

**Verification:**
```python
assert isinstance(t, list)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(t[0], unmasked4D)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye, shape_4d_default

# Workflow
'Test unmask on 4D images.'
data4D = rng.uniform(size=shape_4d_default)
mask = rng.integers(2, size=shape_4d_default[:3], dtype='int32')
mask_img = Nifti1Image(mask, affine_eye)
mask = mask.astype(bool)
masked4D = data4D[mask, :].T
unmasked4D = data4D.copy()
unmasked4D[np.logical_not(mask), :] = 0
t = get_data(unmask(masked4D, mask_img, order='C'))
assert t.ndim == 4
assert t.flags['C_CONTIGUOUS']
assert not t.flags['F_CONTIGUOUS']
assert_array_equal(t, unmasked4D)
t = unmask([masked4D], mask_img, order='F')
t = [get_data(t_) for t_ in t]
assert isinstance(t, list)
assert t[0].ndim == 4
assert not t[0].flags['C_CONTIGUOUS']
assert t[0].flags['F_CONTIGUOUS']
assert_array_equal(t[0], unmasked4D)
```

## Next Steps


---

*Source: test_masking.py:499 | Complexity: Advanced | Last updated: 2026-05-18*