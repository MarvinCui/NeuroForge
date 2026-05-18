# How To: Compute Brain Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test compute_brain_mask.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test compute_brain_mask.'

```python
'Test compute_brain_mask.'
```

**Verification:**
```python
assert (brain_data != 0).any()
```

### Step 2: Assign unknown = data_gen.generate_mni_space_img(...)

```python
img, _ = data_gen.generate_mni_space_img(res=8, random_state=0)
```

**Verification:**
```python
assert (np.logical_and(brain_data, subset) == subset.astype(bool)).all()
```

### Step 3: Assign brain_mask = compute_brain_mask(...)

```python
brain_mask = compute_brain_mask(img, threshold=0.2, verbose=1)
```

**Verification:**
```python
assert (subset != 0).any()
```

### Step 4: Assign gm_mask = compute_brain_mask(...)

```python
gm_mask = compute_brain_mask(img, threshold=0.2, mask_type='gm')
```

**Verification:**
```python
assert (np.logical_and(gm_data, wm_data) == 0).all()
```

### Step 5: Assign wm_mask = compute_brain_mask(...)

```python
wm_mask = compute_brain_mask(img, threshold=0.2, mask_type='wm')
```

**Verification:**
```python
assert (brain_data == get_data(mask_img1)).all()
```

### Step 6: Assign unknown = map(...)

```python
brain_data, gm_data, wm_data = map(get_data, (brain_mask, gm_mask, wm_mask))
```

**Verification:**
```python
assert (brain_data != 0).any()
```

### Step 7: Assign unknown = data_gen.generate_mni_space_img(...)

```python
img1, _ = data_gen.generate_mni_space_img(res=8, random_state=1)
```

### Step 8: Assign mask_img1 = compute_brain_mask(...)

```python
mask_img1 = compute_brain_mask(img1, verbose=1, threshold=0.2)
```

**Verification:**
```python
assert (brain_data == get_data(mask_img1)).all()
```

### Step 9: Call compute_brain_mask()

```python
compute_brain_mask(img, threshold=1)
```

### Step 10: Call compute_brain_mask()

```python
compute_brain_mask(img, verbose=1, mask_type='foo')
```


## Complete Example

```python
# Workflow
'Test compute_brain_mask.'
img, _ = data_gen.generate_mni_space_img(res=8, random_state=0)
brain_mask = compute_brain_mask(img, threshold=0.2, verbose=1)
gm_mask = compute_brain_mask(img, threshold=0.2, mask_type='gm')
wm_mask = compute_brain_mask(img, threshold=0.2, mask_type='wm')
brain_data, gm_data, wm_data = map(get_data, (brain_mask, gm_mask, wm_mask))
assert (brain_data != 0).any()
for subset in (gm_data, wm_data):
    assert (np.logical_and(brain_data, subset) == subset.astype(bool)).all()
    assert (subset != 0).any()
assert (np.logical_and(gm_data, wm_data) == 0).all()
with pytest.warns(MaskWarning):
    compute_brain_mask(img, threshold=1)
img1, _ = data_gen.generate_mni_space_img(res=8, random_state=1)
mask_img1 = compute_brain_mask(img1, verbose=1, threshold=0.2)
assert (brain_data == get_data(mask_img1)).all()
with pytest.raises(ValueError, match='Unknown mask type foo.'):
    compute_brain_mask(img, verbose=1, mask_type='foo')
```

## Next Steps


---

*Source: test_masking.py:299 | Complexity: Advanced | Last updated: 2026-05-18*