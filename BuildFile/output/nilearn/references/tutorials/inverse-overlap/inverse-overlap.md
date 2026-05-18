# How To: Inverse Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Throw error when data to inverse_transform has overlapping data and         allow_overlap=False.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.image`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Throw error when data to inverse_transform has overlapping data and         allow_overlap=False.\n    '

```python
'Throw error when data to inverse_transform has overlapping data and         allow_overlap=False.\n    '
```

**Verification:**
```python
assert_array_almost_equal(get_data(overlap)[1, 1, 1], np.mean(inv_data))
```

### Step 2: Assign shape = value

```python
shape = (5, 5, 5)
```

### Step 3: Assign data = rng.random(...)

```python
data = rng.random((*shape, 5))
```

### Step 4: Assign fmri_img = Nifti1Image(...)

```python
fmri_img = Nifti1Image(data, affine_eye)
```

### Step 5: Assign mask_img = new_img_like(...)

```python
mask_img = new_img_like(fmri_img, np.ones(shape))
```

### Step 6: Assign seeds = value

```python
seeds = [(0, 0, 0), (2, 2, 2)]
```

### Step 7: Assign inv_data = rng.random(...)

```python
inv_data = rng.random(len(seeds))
```

### Step 8: Assign overlapping_masker = NiftiSpheresMasker.fit(...)

```python
overlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=True, mask_img=mask_img).fit()
```

### Step 9: Call overlapping_masker.inverse_transform()

```python
overlapping_masker.inverse_transform(inv_data)
```

### Step 10: Assign overlapping_masker = NiftiSpheresMasker.fit(...)

```python
overlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=True, mask_img=mask_img).fit()
```

### Step 11: Assign overlap = overlapping_masker.inverse_transform(...)

```python
overlap = overlapping_masker.inverse_transform(inv_data)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(get_data(overlap)[1, 1, 1], np.mean(inv_data))
```

### Step 13: Assign noverlapping_masker = NiftiSpheresMasker.fit(...)

```python
noverlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=False, mask_img=mask_img).fit()
```

### Step 14: Call noverlapping_masker.inverse_transform()

```python
noverlapping_masker.inverse_transform(inv_data)
```

### Step 15: Assign noverlapping_masker = NiftiSpheresMasker.fit(...)

```python
noverlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=False, mask_img=mask_img).fit()
```

### Step 16: Call noverlapping_masker.inverse_transform()

```python
noverlapping_masker.inverse_transform(inv_data)
```


## Complete Example

```python
# Setup
# Fixtures: rng, affine_eye

# Workflow
'Throw error when data to inverse_transform has overlapping data and         allow_overlap=False.\n    '
shape = (5, 5, 5)
data = rng.random((*shape, 5))
fmri_img = Nifti1Image(data, affine_eye)
mask_img = new_img_like(fmri_img, np.ones(shape))
seeds = [(0, 0, 0), (2, 2, 2)]
inv_data = rng.random(len(seeds))
overlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=True, mask_img=mask_img).fit()
overlapping_masker.inverse_transform(inv_data)
overlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=True, mask_img=mask_img).fit()
overlap = overlapping_masker.inverse_transform(inv_data)
assert_array_almost_equal(get_data(overlap)[1, 1, 1], np.mean(inv_data))
noverlapping_masker = NiftiSpheresMasker(seeds, radius=1, allow_overlap=False, mask_img=mask_img).fit()
noverlapping_masker.inverse_transform(inv_data)
noverlapping_masker = NiftiSpheresMasker(seeds, radius=2, allow_overlap=False, mask_img=mask_img).fit()
with pytest.raises(ValueError, match='Overlap detected'):
    noverlapping_masker.inverse_transform(inv_data)
```

## Next Steps


---

*Source: test_nifti_spheres_masker.py:330 | Complexity: Advanced | Last updated: 2026-05-18*