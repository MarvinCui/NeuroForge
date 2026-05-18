# How To: Signals Extraction With Labels With Mask Return Masked Atlas

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test masked_atlas is correct in conversion between signals and images     using regions defined by labels and a mask.
    

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
# Fixtures: signals, labels_img, mask_img
```

## Step-by-Step Guide

### Step 1: 'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels and a mask.\n    '

```python
'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels and a mask.\n    '
```

**Verification:**
```python
assert list(np.unique(labels_data_r)) == [0, 1, 2, 5]
```

### Step 2: Assign data_img = signals_to_img_labels(...)

```python
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img, mask_img=mask_img)
```

### Step 3: Assign mask_img = _create_mask_with_3_regions_from_labels_data(...)

```python
mask_img = _create_mask_with_3_regions_from_labels_data(get_data(labels_img), labels_img.affine)
```

### Step 4: Assign unknown = img_to_signals_labels(...)

```python
_, _, masked_atlas_r = img_to_signals_labels(imgs=data_img, labels_img=labels_img, mask_img=mask_img, return_masked_atlas=True)
```

### Step 5: Assign labels_data_r = get_data(...)

```python
labels_data_r = get_data(masked_atlas_r)
```

**Verification:**
```python
assert list(np.unique(labels_data_r)) == [0, 1, 2, 5]
```


## Complete Example

```python
# Setup
# Fixtures: signals, labels_img, mask_img

# Workflow
'Test masked_atlas is correct in conversion between signals and images     using regions defined by labels and a mask.\n    '
data_img = signals_to_img_labels(signals=signals, labels_img=labels_img, mask_img=mask_img)
mask_img = _create_mask_with_3_regions_from_labels_data(get_data(labels_img), labels_img.affine)
_, _, masked_atlas_r = img_to_signals_labels(imgs=data_img, labels_img=labels_img, mask_img=mask_img, return_masked_atlas=True)
labels_data_r = get_data(masked_atlas_r)
assert list(np.unique(labels_data_r)) == [0, 1, 2, 5]
```

## Next Steps


---

*Source: test_signal_extraction.py:458 | Complexity: Intermediate | Last updated: 2026-05-18*