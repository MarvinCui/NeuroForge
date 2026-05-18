# How To: Zeros Affine Diagonal

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test zeros affine diagonal

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `scipy.ndimage`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.regions`
- `nilearn.regions.region_extractor`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: affine_eye, n_regions
```

## Step-by-Step Guide

### Step 1: Assign affine = affine_eye

```python
affine = affine_eye
```

**Verification:**
```python
assert extract_ratio.regions_img_ != ''
```

### Step 2: Assign unknown = value

```python
affine[[0, 1]] = affine[[1, 0]]
```

**Verification:**
```python
assert extract_ratio.regions_img_.shape[-1] >= n_regions
```

### Step 3: Assign unknown = generate_maps(...)

```python
maps, _ = generate_maps(shape=[40, 40, 40], n_regions=n_regions, affine=affine, random_state=42)
```

### Step 4: Assign extract_ratio = RegionExtractor(...)

```python
extract_ratio = RegionExtractor(maps, threshold=0.2, thresholding_strategy='ratio_n_voxels')
```

### Step 5: Call extract_ratio.fit()

```python
extract_ratio.fit()
```

**Verification:**
```python
assert extract_ratio.regions_img_ != ''
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, n_regions

# Workflow
affine = affine_eye
affine[[0, 1]] = affine[[1, 0]]
maps, _ = generate_maps(shape=[40, 40, 40], n_regions=n_regions, affine=affine, random_state=42)
extract_ratio = RegionExtractor(maps, threshold=0.2, thresholding_strategy='ratio_n_voxels')
extract_ratio.fit()
assert extract_ratio.regions_img_ != ''
assert extract_ratio.regions_img_.shape[-1] >= n_regions
```

## Next Steps


---

*Source: test_region_extractor.py:405 | Complexity: Intermediate | Last updated: 2026-05-18*