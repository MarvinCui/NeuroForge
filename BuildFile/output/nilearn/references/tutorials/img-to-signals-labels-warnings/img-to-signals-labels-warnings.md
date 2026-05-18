# How To: Img To Signals Labels Warnings

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test img to signals labels warnings

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
# Fixtures: labeled_regions, fmri_img
```

## Step-by-Step Guide

### Step 1: Assign labels_data = get_data(...)

```python
labels_data = get_data(labeled_regions)
```

**Verification:**
```python
assert labels_signals.shape == (N_TIMEPOINTS, 3)
```

### Step 2: Assign mask_img = _create_mask_with_3_regions_from_labels_data(...)

```python
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
```

**Verification:**
```python
assert len(labels_labels) == 3
```

### Step 3: Assign unknown = img_to_signals_labels(...)

```python
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=False)
```

**Verification:**
```python
assert labels_signals.shape == (N_TIMEPOINTS, 8)
```

### Step 4: Assign unknown = img_to_signals_labels(...)

```python
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=True)
```

**Verification:**
```python
assert len(labels_labels) == 8
```

### Step 5: Call img_to_signals_labels()

```python
img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=False, return_masked_atlas=False)
```


## Complete Example

```python
# Setup
# Fixtures: labeled_regions, fmri_img

# Workflow
labels_data = get_data(labeled_regions)
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labeled_regions.affine)
with pytest.warns(UserWarning, match='After applying mask to the labels image, the following labels were removed: \\{3, 4, 6, 7, 8\\}. Out of 9 labels, the masked labels image only contains 4 labels \\(including background\\).'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=False)
assert labels_signals.shape == (N_TIMEPOINTS, 3)
assert len(labels_labels) == 3
with pytest.warns(FutureWarning, match='"keep_masked_labels" parameter will be removed.'):
    labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=True)
assert labels_signals.shape == (N_TIMEPOINTS, 8)
assert len(labels_labels) == 8
with pytest.warns(FutureWarning, match='In version 0.15, "return_masked_atlas" parameter will be removed.'):
    img_to_signals_labels(imgs=fmri_img, labels_img=labeled_regions, mask_img=mask_img, keep_masked_labels=False, return_masked_atlas=False)
```

## Next Steps


---

*Source: test_signal_extraction.py:587 | Complexity: Intermediate | Last updated: 2026-05-18*