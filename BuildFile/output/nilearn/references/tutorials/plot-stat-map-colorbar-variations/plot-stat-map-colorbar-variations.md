# How To: Plot Stat Map Colorbar Variations

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Smoke test for plot_stat_map with different colorbar configurations.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`
- `nilearn.image.resampling`
- `nilearn.plotting`
- `nilearn.plotting.find_cuts`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, params, img_3d_mni, affine_mni, rng
```

## Step-by-Step Guide

### Step 1: 'Smoke test for plot_stat_map with different colorbar configurations.'

```python
'Smoke test for plot_stat_map with different colorbar configurations.'
```

### Step 2: Assign data_positive = get_data(...)

```python
data_positive = get_data(img_3d_mni)
```

### Step 3: Assign data_negative = value

```python
data_negative = -data_positive
```

### Step 4: Assign img_negative = Nifti1Image(...)

```python
img_negative = Nifti1Image(data_negative, affine_mni)
```

### Step 5: Assign data_heterogeneous = value

```python
data_heterogeneous = data_positive * rng.standard_normal(size=data_positive.shape)
```

### Step 6: Assign img_heterogeneous = Nifti1Image(...)

```python
img_heterogeneous = Nifti1Image(data_heterogeneous, affine_mni)
```

### Step 7: Call plot_stat_map()

```python
plot_stat_map(img, cut_coords=(-90, -125, -70), **params)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, params, img_3d_mni, affine_mni, rng

# Workflow
'Smoke test for plot_stat_map with different colorbar configurations.'
data_positive = get_data(img_3d_mni)
data_negative = -data_positive
img_negative = Nifti1Image(data_negative, affine_mni)
data_heterogeneous = data_positive * rng.standard_normal(size=data_positive.shape)
img_heterogeneous = Nifti1Image(data_heterogeneous, affine_mni)
for img in [img_3d_mni, img_negative, img_heterogeneous]:
    plot_stat_map(img, cut_coords=(-90, -125, -70), **params)
```

## Next Steps


---

*Source: test_plot_stat_map.py:142 | Complexity: Intermediate | Last updated: 2026-05-18*