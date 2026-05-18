# How To: Outlier Cut Coords

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test to plot a subset of a large set of cuts found for a small area.

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
# Fixtures: matplotlib_pyplot
```

## Step-by-Step Guide

### Step 1: 'Test to plot a subset of a large set of cuts found for a small area.'

```python
'Test to plot a subset of a large set of cuts found for a small area.'
```

### Step 2: Assign bg_img = load_mni152_template(...)

```python
bg_img = load_mni152_template(resolution=2)
```

### Step 3: Assign data = np.zeros(...)

```python
data = np.zeros((79, 95, 79))
```

### Step 4: Assign affine = value

```python
affine = bg_img.affine
```

### Step 5: Assign unknown = value

```python
x, y, z = (20, 22, 60)
```

### Step 6: Assign unknown = coord_transform(...)

```python
x_map, y_map, z_map = coord_transform(x, y, z, np.linalg.inv(affine))
```

### Step 7: Assign unknown = 1

```python
data[int(x_map) - 1:int(x_map) + 1, int(y_map) - 1:int(y_map) + 1, int(z_map) - 1:int(z_map) + 1] = 1
```

### Step 8: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine)
```

### Step 9: Assign cuts = find_cut_slices(...)

```python
cuts = find_cut_slices(img, n_cuts=20, direction='z')
```

### Step 10: Call plot_stat_map()

```python
plot_stat_map(img, display_mode='z', cut_coords=cuts, bg_img=bg_img)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot

# Workflow
'Test to plot a subset of a large set of cuts found for a small area.'
bg_img = load_mni152_template(resolution=2)
data = np.zeros((79, 95, 79))
affine = bg_img.affine
x, y, z = (20, 22, 60)
x_map, y_map, z_map = coord_transform(x, y, z, np.linalg.inv(affine))
data[int(x_map) - 1:int(x_map) + 1, int(y_map) - 1:int(y_map) + 1, int(z_map) - 1:int(z_map) + 1] = 1
img = Nifti1Image(data, affine)
cuts = find_cut_slices(img, n_cuts=20, direction='z')
with pytest.warns(UserWarning, match='seem to be out of the image'):
    plot_stat_map(img, display_mode='z', cut_coords=cuts, bg_img=bg_img)
```

## Next Steps


---

*Source: test_plot_stat_map.py:176 | Complexity: Advanced | Last updated: 2026-05-18*