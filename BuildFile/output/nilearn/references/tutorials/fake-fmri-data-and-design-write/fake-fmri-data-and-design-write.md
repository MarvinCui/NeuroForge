# How To: Fake Fmri Data And Design Write

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fake fmri data and design write

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `pandas.api.types`
- `pandas.testing`
- `nilearn._utils.data_gen`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path, shapes, rank, affine
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rank, affine=affine, random_state=42)
```

**Verification:**
```python
assert_almost_equal(mask_img.get_fdata(), mask.get_fdata())
```

### Step 2: Assign unknown = write_fake_fmri_data_and_design(...)

```python
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk=rank, affine=affine, random_state=42, file_path=tmp_path)
```

**Verification:**
```python
assert_almost_equal(mask_img.affine, mask.affine)
```

### Step 3: Assign mask_img = load(...)

```python
mask_img = load(mask_file)
```

**Verification:**
```python
assert_almost_equal(fmri_img.get_fdata(), fmri.get_fdata())
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(mask_img.get_fdata(), mask.get_fdata())
```

**Verification:**
```python
assert_almost_equal(fmri_img.affine, fmri.affine)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(mask_img.affine, mask.affine)
```

**Verification:**
```python
assert_frame_equal(pd.read_csv(design_file, sep='\t'), design, check_exact=False)
```

### Step 6: Assign fmri_img = load(...)

```python
fmri_img = load(fmri_file)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(fmri_img.get_fdata(), fmri.get_fdata())
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(fmri_img.affine, fmri.affine)
```

### Step 9: Call assert_frame_equal()

```python
assert_frame_equal(pd.read_csv(design_file, sep='\t'), design, check_exact=False)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, shapes, rank, affine

# Workflow
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rank, affine=affine, random_state=42)
mask_file, fmri_files, design_files = write_fake_fmri_data_and_design(shapes, rk=rank, affine=affine, random_state=42, file_path=tmp_path)
mask_img = load(mask_file)
assert_almost_equal(mask_img.get_fdata(), mask.get_fdata())
assert_almost_equal(mask_img.affine, mask.affine)
for fmri_file, fmri in zip(fmri_files, fmri_data, strict=False):
    fmri_img = load(fmri_file)
    assert_almost_equal(fmri_img.get_fdata(), fmri.get_fdata())
    assert_almost_equal(fmri_img.affine, fmri.affine)
for design_file, design in zip(design_files, design_matrices, strict=False):
    assert_frame_equal(pd.read_csv(design_file, sep='\t'), design, check_exact=False)
```

## Next Steps


---

*Source: test_data_gen.py:609 | Complexity: Advanced | Last updated: 2026-05-18*