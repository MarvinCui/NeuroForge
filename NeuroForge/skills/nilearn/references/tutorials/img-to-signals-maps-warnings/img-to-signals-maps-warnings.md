# How To: Img To Signals Maps Warnings

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test img to signals maps warnings

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn._utils.data_gen`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.regions.signal_extraction`

**Setup Required:**
```python
# Fixtures: labeled_regions, fmri_img, shape_3d_default
```

## Step-by-Step Guide

### Step 1: Assign labels = list(...)

```python
labels = list(range(N_REGIONS + 1))
```

**Verification:**
```python
assert maps_signals.shape == (N_TIMEPOINTS, 3)
```

### Step 2: Assign labels_data = get_data(...)

```python
labels_data = get_data(labeled_regions)
```

**Verification:**
```python
assert len(maps_labels) == 3
```

### Step 3: Assign maps_data = np.zeros(...)

```python
maps_data = np.zeros((*shape_3d_default, N_REGIONS))
```

**Verification:**
```python
assert maps_signals.shape == (N_TIMEPOINTS, 8)
```

### Step 4: Assign maps_img = Nifti1Image(...)

```python
maps_img = Nifti1Image(maps_data, labeled_regions.affine)
```

**Verification:**
```python
assert len(maps_labels) == 8
```

### Step 5: Assign mask_img = _create_mask_with_3_regions_from_labels_data(...)

```python
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
```

**Verification:**
```python
assert maps_signals.shape == (N_TIMEPOINTS, 3)
```

### Step 6: Assign unknown = 1

```python
maps_data[labels_data == l, n - 1] = 1
```

### Step 7: Assign unknown = img_to_signals_maps(...)

```python
maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img)
```

### Step 8: Assign unknown = img_to_signals_maps(...)

```python
maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img, keep_masked_maps=True)
```


## Complete Example

```python
# Setup
# Fixtures: labeled_regions, fmri_img, shape_3d_default

# Workflow
labels = list(range(N_REGIONS + 1))
labels_data = get_data(labeled_regions)
maps_data = np.zeros((*shape_3d_default, N_REGIONS))
for n, l in enumerate(labels):
    if n == 0:
        continue
    maps_data[labels_data == l, n - 1] = 1
maps_img = Nifti1Image(maps_data, labeled_regions.affine)
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
with pytest.warns(UserWarning, match='After applying mask to the maps image, maps with the following indices were removed: \\{2, 3, 5, 6, 7\\}. Out of 8 maps, the masked map image only contains 3 maps.'):
    maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img)
assert maps_signals.shape == (N_TIMEPOINTS, 3)
assert len(maps_labels) == 3
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img, keep_masked_maps=True)
assert maps_signals.shape == (N_TIMEPOINTS, 8)
assert len(maps_labels) == 8
```

## Next Steps


---

*Source: test_signal_extraction.py:656 | Complexity: Advanced | Last updated: 2026-05-18*