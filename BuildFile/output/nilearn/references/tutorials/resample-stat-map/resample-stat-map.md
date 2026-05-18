# How To: Resample Stat Map

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test resample stat map

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `io`
- `numpy`
- `pytest`
- `matplotlib`
- `nibabel`
- `nilearn`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.html_stat_map`

**Setup Required:**
```python
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: Assign unknown = _simulate_img(...)

```python
bg_img, data = _simulate_img()
```

**Verification:**
```python
assert stat_map_img.affine[0, 0] == bg_img.affine[0, 0], 'stat_map_img was not resampled at the resolution of background'
```

### Step 2: Assign affine = value

```python
affine = 2 * affine_eye
```

**Verification:**
```python
assert mask_img.affine[0, 0] == bg_img.affine[0, 0], 'mask_img was not resampled at the resolution of background'
```

### Step 3: Assign unknown = 1

```python
affine[3, 3] = 1
```

### Step 4: Assign unknown = 0.1

```python
affine[0, 1] = 0.1
```

### Step 5: Assign stat_map_img = Nifti1Image(...)

```python
stat_map_img = Nifti1Image(data, affine)
```

### Step 6: Assign mask_img = new_img_like(...)

```python
mask_img = new_img_like(stat_map_img, data > 0, stat_map_img.affine)
```

### Step 7: Assign unknown = _resample_stat_map(...)

```python
stat_map_img, mask_img = _resample_stat_map(stat_map_img, bg_img, mask_img, resampling_interpolation='nearest')
```

### Step 8: Call _check_affine()

```python
_check_affine(stat_map_img.affine)
```

### Step 9: Call _check_affine()

```python
_check_affine(mask_img.affine)
```

**Verification:**
```python
assert stat_map_img.affine[0, 0] == bg_img.affine[0, 0], 'stat_map_img was not resampled at the resolution of background'
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
bg_img, data = _simulate_img()
affine = 2 * affine_eye
affine[3, 3] = 1
affine[0, 1] = 0.1
stat_map_img = Nifti1Image(data, affine)
mask_img = new_img_like(stat_map_img, data > 0, stat_map_img.affine)
stat_map_img, mask_img = _resample_stat_map(stat_map_img, bg_img, mask_img, resampling_interpolation='nearest')
_check_affine(stat_map_img.affine)
_check_affine(mask_img.affine)
assert stat_map_img.affine[0, 0] == bg_img.affine[0, 0], 'stat_map_img was not resampled at the resolution of background'
assert mask_img.affine[0, 0] == bg_img.affine[0, 0], 'mask_img was not resampled at the resolution of background'
```

## Next Steps


---

*Source: test_html_stat_map.py:216 | Complexity: Advanced | Last updated: 2026-05-18*