# How To: Plot Carpet With Atlas

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_carpet when using an atlas.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, img_4d_mni, img_atlas
```

## Step-by-Step Guide

### Step 1: 'Test plot_carpet when using an atlas.'

```python
'Test plot_carpet when using an atlas.'
```

**Verification:**
```python
assert len(display.axes) == 2
```

### Step 2: Assign display = plot_carpet(...)

```python
display = plot_carpet(img_4d_mni, mask_img=img_atlas['img'], t_r=2, detrend=False, title='TEST', standardize='zscore_sample')
```

**Verification:**
```python
assert ax.get_ylabel() == 'voxels'
```

### Step 3: Assign ax = value

```python
ax = display.axes[1]
```

**Verification:**
```python
assert len(np.unique(colorbar)) == len(img_atlas['labels'])
```

### Step 4: Assign ax = value

```python
ax = display.axes[0]
```

### Step 5: Assign colorbar = unknown.get_array(...)

```python
colorbar = ax.images[0].get_array()
```

**Verification:**
```python
assert len(np.unique(colorbar)) == len(img_atlas['labels'])
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, img_4d_mni, img_atlas

# Workflow
'Test plot_carpet when using an atlas.'
display = plot_carpet(img_4d_mni, mask_img=img_atlas['img'], t_r=2, detrend=False, title='TEST', standardize='zscore_sample')
assert len(display.axes) == 2
ax = display.axes[1]
assert ax.get_ylabel() == 'voxels'
ax = display.axes[0]
colorbar = ax.images[0].get_array()
assert len(np.unique(colorbar)) == len(img_atlas['labels'])
```

## Next Steps


---

*Source: test_plot_carpet.py:62 | Complexity: Intermediate | Last updated: 2026-05-18*