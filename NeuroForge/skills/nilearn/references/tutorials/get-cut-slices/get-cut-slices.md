# How To: Get Cut Slices

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get cut slices

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
img, data = _simulate_img()
```

**Verification:**
```python
assert (cut_slices == [4, 4, 4]).all()
```

### Step 2: Assign cut_slices = _get_cut_slices(...)

```python
cut_slices = _get_cut_slices(img, cut_coords=None, threshold=None)
```

**Verification:**
```python
assert (cut_slices == [2, 2, 2]).all()
```

### Step 3: Assign cut_slices = _get_cut_slices(...)

```python
cut_slices = _get_cut_slices(img, cut_coords=[2, 2, 2], threshold=None)
```

**Verification:**
```python
assert (cut_slices == [4, 4, 4]).all()
```

### Step 4: Assign affine = value

```python
affine = 2 * affine_eye
```

### Step 5: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

### Step 6: Assign cut_slices = _get_cut_slices(...)

```python
cut_slices = _get_cut_slices(img, cut_coords=None, threshold=None)
```

**Verification:**
```python
assert (cut_slices == [4, 4, 4]).all()
```

### Step 7: Call _get_cut_slices()

```python
_get_cut_slices(img, cut_coords=4, threshold=None)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
img, data = _simulate_img()
cut_slices = _get_cut_slices(img, cut_coords=None, threshold=None)
assert (cut_slices == [4, 4, 4]).all()
with pytest.raises(ValueError):
    _get_cut_slices(img, cut_coords=4, threshold=None)
cut_slices = _get_cut_slices(img, cut_coords=[2, 2, 2], threshold=None)
assert (cut_slices == [2, 2, 2]).all()
affine = 2 * affine_eye
img = Nifti1Image(data, affine)
cut_slices = _get_cut_slices(img, cut_coords=None, threshold=None)
assert (cut_slices == [4, 4, 4]).all()
```

## Next Steps


---

*Source: test_html_stat_map.py:350 | Complexity: Intermediate | Last updated: 2026-05-18*