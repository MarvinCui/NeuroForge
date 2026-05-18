# How To: Signal Extraction Nans In Regions Are Replaced With Zeros

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test signal extraction nans in regions are replaced with zeros

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (4, 5, 6)
```

**Verification:**
```python
assert np.all(labels_signals[:, labels_labels.index(2)] == 0.0)
```

### Step 2: Assign labels = list(...)

```python
labels = list(range(N_REGIONS + 1))
```

### Step 3: Assign labels_img = generate_labeled_regions(...)

```python
labels_img = generate_labeled_regions(shape, N_REGIONS, labels=labels)
```

### Step 4: Assign labels_data = get_data(...)

```python
labels_data = get_data(labels_img)
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
fmri_img, _ = generate_fake_fmri(shape=shape, affine=labels_img.affine, length=N_TIMEPOINTS)
```

### Step 6: Assign mask_img = _create_mask_with_3_regions_from_labels_data(...)

```python
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labels_img.affine)
```

### Step 7: Assign region1 = value

```python
region1 = labels_data == 2
```

### Step 8: Assign indices = tuple(...)

```python
indices = tuple((ind[:1] for ind in np.where(region1)))
```

### Step 9: Assign unknown = value

```python
get_data(fmri_img)[indices] = np.nan
```

### Step 10: Assign unknown = img_to_signals_labels(...)

```python
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labels_img, mask_img=mask_img)
```

**Verification:**
```python
assert np.all(labels_signals[:, labels_labels.index(2)] == 0.0)
```


## Complete Example

```python
# Workflow
shape = (4, 5, 6)
labels = list(range(N_REGIONS + 1))
labels_img = generate_labeled_regions(shape, N_REGIONS, labels=labels)
labels_data = get_data(labels_img)
fmri_img, _ = generate_fake_fmri(shape=shape, affine=labels_img.affine, length=N_TIMEPOINTS)
mask_img = _create_mask_with_3_regions_from_labels_data(labels_data, labels_img.affine)
region1 = labels_data == 2
indices = tuple((ind[:1] for ind in np.where(region1)))
get_data(fmri_img)[indices] = np.nan
labels_signals, labels_labels, _ = img_to_signals_labels(imgs=fmri_img, labels_img=labels_img, mask_img=mask_img)
assert np.all(labels_signals[:, labels_labels.index(2)] == 0.0)
```

## Next Steps


---

*Source: test_signal_extraction.py:714 | Complexity: Advanced | Last updated: 2026-05-18*