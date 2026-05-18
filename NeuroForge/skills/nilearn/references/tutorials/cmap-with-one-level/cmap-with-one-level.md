# How To: Cmap With One Level

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test we can handle cmap with only 1 level.

Regression test for
https://github.com/nilearn/nilearn/issues/4255

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `nilearn._utils.bids`
- `nilearn.conftest`
- `nilearn.image.resampling`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, shape_3d_default, affine_eye
```

## Step-by-Step Guide

### Step 1: 'Test we can handle cmap with only 1 level.\n\n    Regression test for\n    https://github.com/nilearn/nilearn/issues/4255\n    '

```python
'Test we can handle cmap with only 1 level.\n\n    Regression test for\n    https://github.com/nilearn/nilearn/issues/4255\n    '
```

### Step 2: Assign array_data = np.zeros(...)

```python
array_data = np.zeros(shape_3d_default)
```

### Step 3: Assign unknown = 1

```python
array_data[0, 1, 1] = 1
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(array_data, affine_eye)
```

### Step 5: Assign clust_ids = list(...)

```python
clust_ids = list(np.unique(img.get_fdata())[1:])
```

### Step 6: Assign cmap = plt.get_cmap(...)

```python
cmap = plt.get_cmap('tab20', len(clust_ids))
```

### Step 7: Call plot_roi()

```python
plot_roi(img, alpha=0.8, colorbar=True, cmap=cmap)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, shape_3d_default, affine_eye

# Workflow
'Test we can handle cmap with only 1 level.\n\n    Regression test for\n    https://github.com/nilearn/nilearn/issues/4255\n    '
array_data = np.zeros(shape_3d_default)
array_data[0, 1, 1] = 1
img = Nifti1Image(array_data, affine_eye)
clust_ids = list(np.unique(img.get_fdata())[1:])
cmap = plt.get_cmap('tab20', len(clust_ids))
plot_roi(img, alpha=0.8, colorbar=True, cmap=cmap)
```

## Next Steps


---

*Source: test_plot_roi.py:95 | Complexity: Intermediate | Last updated: 2026-05-18*