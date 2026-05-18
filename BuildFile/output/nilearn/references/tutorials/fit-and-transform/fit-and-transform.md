# How To: Fit And Transform

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fit and transform

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
# Fixtures: maps_and_mask
```

## Step-by-Step Guide

### Step 1: Assign unknown = maps_and_mask

```python
maps, mask_img = maps_and_mask
```

**Verification:**
```python
assert not np.all(get_data(extractor_without_mask.regions_img_)[mask_data == 0] == 0.0)
```

### Step 2: Assign mask_data = get_data(...)

```python
mask_data = get_data(mask_img)
```

**Verification:**
```python
assert np.all(get_data(extractor_with_mask.regions_img_)[mask_data == 0] == 0.0)
```

### Step 3: Assign unknown = 0

```python
mask_data[1, 1, 1] = 0
```

### Step 4: Assign extractor_without_mask = RegionExtractor(...)

```python
extractor_without_mask = RegionExtractor(maps)
```

### Step 5: Call extractor_without_mask.fit()

```python
extractor_without_mask.fit()
```

### Step 6: Assign extractor_with_mask = RegionExtractor(...)

```python
extractor_with_mask = RegionExtractor(maps, mask_img=mask_img)
```

### Step 7: Call extractor_with_mask.fit()

```python
extractor_with_mask.fit()
```

**Verification:**
```python
assert not np.all(get_data(extractor_without_mask.regions_img_)[mask_data == 0] == 0.0)
```


## Complete Example

```python
# Setup
# Fixtures: maps_and_mask

# Workflow
maps, mask_img = maps_and_mask
mask_data = get_data(mask_img)
mask_data[1, 1, 1] = 0
extractor_without_mask = RegionExtractor(maps)
extractor_without_mask.fit()
extractor_with_mask = RegionExtractor(maps, mask_img=mask_img)
extractor_with_mask.fit()
assert not np.all(get_data(extractor_without_mask.regions_img_)[mask_data == 0] == 0.0)
assert np.all(get_data(extractor_with_mask.regions_img_)[mask_data == 0] == 0.0)
```

## Next Steps


---

*Source: test_region_extractor.py:296 | Complexity: Intermediate | Last updated: 2026-05-18*