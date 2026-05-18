# How To: Find Parcellation Cut Coords Non Trivial Affine

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test find_parcellation_cut_coords with non-trivial affine.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `nilearn.masking`
- `nilearn.plotting.find_cuts`


## Step-by-Step Guide

### Step 1: 'Test find_parcellation_cut_coords with non-trivial affine.'

```python
'Test find_parcellation_cut_coords with non-trivial affine.'
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
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a / 2.0, y_map_a / 3.0, z_map_a / 4.0), rtol=0.06)
```

### Step 3: Assign unknown = value

```python
x_map_b, y_map_b, z_map_b = (30, 30, 30)
```

**Verification:**
```python
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b / 2.0, y_map_b / 3.0, z_map_b / 4.0), rtol=0.06)
```

### Step 4: Assign unknown = value

```python
x_map_c, y_map_c, z_map_c = (50, 50, 50)
```

**Verification:**
```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c / 2.0, y_map_c / 3.0, z_map_c / 4.0), rtol=0.06)
```

### Step 5: Assign data = _parcellation_3_roi(...)

```python
data = _parcellation_3_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b, x_map_c, y_map_c, z_map_c)
```

### Step 6: Assign labels = np.unique(...)

```python
labels = np.unique(data)
```

### Step 7: Assign labels = value

```python
labels = labels[labels != 0]
```

### Step 8: Assign n_labels = len(...)

```python
n_labels = len(labels)
```

### Step 9: Assign affine = np.diag(...)

```python
affine = np.diag([1 / 2.0, 1 / 3.0, 1 / 4.0, 1.0])
```

### Step 10: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

### Step 11: Assign coords = find_parcellation_cut_coords(...)

```python
coords = find_parcellation_cut_coords(img)
```

**Verification:**
```python
assert (n_labels, 3) == coords.shape
```

### Step 12: Call assert_allclose()

```python
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a / 2.0, y_map_a / 3.0, z_map_a / 4.0), rtol=0.06)
```

### Step 13: Call assert_allclose()

```python
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b / 2.0, y_map_b / 3.0, z_map_b / 4.0), rtol=0.06)
```

### Step 14: Call assert_allclose()

```python
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c / 2.0, y_map_c / 3.0, z_map_c / 4.0), rtol=0.06)
```


## Complete Example

```python
# Workflow
'Test find_parcellation_cut_coords with non-trivial affine.'
x_map_a, y_map_a, z_map_a = (10, 10, 10)
x_map_b, y_map_b, z_map_b = (30, 30, 30)
x_map_c, y_map_c, z_map_c = (50, 50, 50)
data = _parcellation_3_roi(x_map_a, y_map_a, z_map_a, x_map_b, y_map_b, z_map_b, x_map_c, y_map_c, z_map_c)
labels = np.unique(data)
labels = labels[labels != 0]
n_labels = len(labels)
affine = np.diag([1 / 2.0, 1 / 3.0, 1 / 4.0, 1.0])
img = Nifti1Image(data, affine)
coords = find_parcellation_cut_coords(img)
assert (n_labels, 3) == coords.shape
assert_allclose((coords[0][0], coords[0][1], coords[0][2]), (x_map_a / 2.0, y_map_a / 3.0, z_map_a / 4.0), rtol=0.06)
assert_allclose((coords[1][0], coords[1][1], coords[1][2]), (x_map_b / 2.0, y_map_b / 3.0, z_map_b / 4.0), rtol=0.06)
assert_allclose((coords[2][0], coords[2][1], coords[2][2]), (x_map_c / 2.0, y_map_c / 3.0, z_map_c / 4.0), rtol=0.06)
```

## Next Steps


---

*Source: test_find_cuts.py:421 | Complexity: Advanced | Last updated: 2026-05-18*