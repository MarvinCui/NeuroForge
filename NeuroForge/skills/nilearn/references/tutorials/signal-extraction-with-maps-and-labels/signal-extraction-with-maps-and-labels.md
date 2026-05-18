# How To: Signal Extraction With Maps And Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test signal extraction with maps and labels

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
assert_almost_equal(maps_signals, labels_signals)
```

### Step 2: Assign labels_data = get_data(...)

```python
labels_data = get_data(labeled_regions)
```

**Verification:**
```python
assert_almost_equal(maps_signals, labels_signals)
```

### Step 3: Assign maps_data = np.zeros(...)

```python
maps_data = np.zeros((*shape_3d_default, N_REGIONS))
```

**Verification:**
```python
assert maps_signals.shape[1] == N_REGIONS
```

### Step 4: Assign maps_img = Nifti1Image(...)

```python
maps_img = Nifti1Image(maps_data, labeled_regions.affine)
```

**Verification:**
```python
assert maps_labels == list(range(len(maps_labels)))
```

### Step 5: Assign unknown = img_to_signals_maps(...)

```python
maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, keep_masked_maps=True)
```

**Verification:**
```python
assert labels_signals.shape == (N_TIMEPOINTS, N_REGIONS)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(maps_signals, labels_signals)
```

**Verification:**
```python
assert labels_labels == labels[1:]
```

### Step 7: Assign mask_img = _create_mask_with_3_regions_from_labels_data(...)

```python
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
```

**Verification:**
```python
assert labels_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(maps_signals, labels_signals)
```

**Verification:**
```python
assert maps_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

### Step 9: Assign labels_img_r = signals_to_img_labels(...)

```python
labels_img_r = signals_to_img_labels(labels_signals, labeled_regions, mask_img=mask_img)
```

**Verification:**
```python
assert labels_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

### Step 10: Assign maps_img_r = signals_to_img_maps(...)

```python
maps_img_r = signals_to_img_maps(maps_signals, maps_img, mask_img=mask_img)
```

**Verification:**
```python
assert maps_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

### Step 11: Assign unknown = 1

```python
maps_data[labels_data == l, n - 1] = 1
```

### Step 12: Assign unknown = img_to_signals_labels(...)

```python
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, keep_masked_labels=True)
```

### Step 13: Assign unknown = img_to_signals_labels(...)

```python
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=True)
```

### Step 14: Assign unknown = img_to_signals_maps(...)

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
maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, keep_masked_maps=True)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, keep_masked_labels=True)
assert_almost_equal(maps_signals, labels_signals)
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=True)
with pytest.warns(FutureWarning, match='"keep_masked_maps" parameter will be removed'):
    maps_signals, maps_labels = img_to_signals_maps(fmri_img, maps_img, mask_img=mask_img, keep_masked_maps=True)
assert_almost_equal(maps_signals, labels_signals)
assert maps_signals.shape[1] == N_REGIONS
assert maps_labels == list(range(len(maps_labels)))
assert labels_signals.shape == (N_TIMEPOINTS, N_REGIONS)
assert labels_labels == labels[1:]
labels_img_r = signals_to_img_labels(labels_signals, labeled_regions, mask_img=mask_img)
assert labels_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
maps_img_r = signals_to_img_maps(maps_signals, maps_img, mask_img=mask_img)
assert maps_img_r.shape == (*shape_3d_default, N_TIMEPOINTS)
```

## Next Steps


---

*Source: test_signal_extraction.py:524 | Complexity: Advanced | Last updated: 2026-05-18*