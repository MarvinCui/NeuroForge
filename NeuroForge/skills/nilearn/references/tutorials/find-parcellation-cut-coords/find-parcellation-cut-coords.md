# How To: Find Parcellation Cut Coords

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test find_parcellation_cut_coords on simple affine.

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
# Fixtures: affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test find_parcellation_cut_coords on simple affine.'

```python
'Test find_parcellation_cut_coords on simple affine.'
```

**Verification:**
```python
assert (n_labels, 3) == coords.shape
```

### Step 2: Assign unknown = value

```python
x_map_a, y_map_a, z_map_a = (10, 10, 10)
```

**Verification:**
```python
assert n_labels == len(labels_list)
```

### Step 3: Assign unknown = value

```python
x_map_b, y_map_b, z_map_b = (30, 30, 30)
```

**Verification:**
```python
assert list(labels) == labels_list
```

### Step 4: Assign unknown = value

```python
x_map_c, y_map_c, z_map_c = (50, 50, 50)
```

**Verification:**
```python
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
```

### Step 5: Assign data = _parcellation_3_roi(...)

```python
data = _parcellation_3_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b, x_map_c, y_map_c, z_map_c)
```

**Verification:**
```python
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b, y_map_b, z_map_b), rtol=0.06)
```

### Step 6: Assign labels = np.unique(...)

```python
labels = np.unique(data)
```

**Verification:**
```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c, y_map_c, z_map_c), rtol=0.06)
```

### Step 7: Assign labels = value

```python
labels = labels[labels != 0]
```

### Step 8: Assign n_labels = len(...)

```python
n_labels = len(labels)
```

### Step 9: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 10: Assign unknown = find_parcellation_cut_coords(...)

```python
coords, labels_list = find_parcellation_cut_coords(img, return_label_names=True)
```

**Verification:**
```python
assert (n_labels, 3) == coords.shape
```

### Step 11: Call assert_allclose()

```python
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
```

### Step 12: Call assert_allclose()

```python
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b, y_map_b, z_map_b), rtol=0.06)
```

### Step 13: Call assert_allclose()

```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c, y_map_c, z_map_c), rtol=0.06)
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye

# Workflow
'Test find_parcellation_cut_coords on simple affine.'
x_map_a, y_map_a, z_map_a = (10, 10, 10)
x_map_b, y_map_b, z_map_b = (30, 30, 30)
x_map_c, y_map_c, z_map_c = (50, 50, 50)
data = _parcellation_3_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b, x_map_c, y_map_c, z_map_c)
labels = np.unique(data)
labels = labels[labels != 0]
n_labels = len(labels)
img = Nifti1Image(data, affine_eye)
coords, labels_list = find_parcellation_cut_coords(img, return_label_names=True)
assert (n_labels, 3) == coords.shape
assert n_labels == len(labels_list)
assert list(labels) == labels_list
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a, y_map_a, z_map_a), rtol=0.06)
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b, y_map_b, z_map_b), rtol=0.06)
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c, y_map_c, z_map_c), rtol=0.06)
```

## Next Steps


---

*Source: test_find_cuts.py:365 | Complexity: Advanced | Last updated: 2026-05-18*