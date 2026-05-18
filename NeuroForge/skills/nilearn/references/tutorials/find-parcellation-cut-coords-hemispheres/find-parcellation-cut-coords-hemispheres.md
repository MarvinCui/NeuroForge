# How To: Find Parcellation Cut Coords Hemispheres

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find parcellation cut coords hemispheres

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn.masking`
- `nilearn.plotting.find_cuts`

**Setup Required:**
```python
# Fixtures: affine_mni
```

## Step-by-Step Guide

### Step 1: Assign data = np.zeros(...)

```python
data = np.zeros((10, 10, 10))
```

**Verification:**
```python
assert len(coords) == 1
```

### Step 2: Assign unknown = 1

```python
data[2:5, 2:5, 2:5] = 1
```

**Verification:**
```python
assert labels == [1]
```

### Step 3: Assign labels_img = Nifti1Image(...)

```python
labels_img = Nifti1Image(data, affine_mni)
```

**Verification:**
```python
assert len(coords) == 1
```

### Step 4: Assign unknown = find_parcellation_cut_coords(...)

```python
coords, labels = find_parcellation_cut_coords(labels_img, return_label_names=True, label_hemisphere='left')
```

**Verification:**
```python
assert labels == [1]
```

### Step 5: Assign unknown = find_parcellation_cut_coords(...)

```python
coords, labels = find_parcellation_cut_coords(labels_img, return_label_names=True, label_hemisphere='right')
```

**Verification:**
```python
assert len(coords) == 1
```


## Complete Example

```python
# Setup
# Fixtures: affine_mni

# Workflow
data = np.zeros((10, 10, 10))
data[2:5, 2:5, 2:5] = 1
labels_img = Nifti1Image(data, affine_mni)
coords, labels = find_parcellation_cut_coords(labels_img, return_label_names=True, label_hemisphere='left')
assert len(coords) == 1
assert labels == [1]
coords, labels = find_parcellation_cut_coords(labels_img, return_label_names=True, label_hemisphere='right')
assert len(coords) == 1
assert labels == [1]
```

## Next Steps


---

*Source: test_find_cuts.py:475 | Complexity: Intermediate | Last updated: 2026-05-18*