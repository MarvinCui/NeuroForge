# How To: Plot Carpet Long Acquisition

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check contents of plot_carpet for img with many volumes.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, img_3d_ones_mni, img_4d_long_mni
```

## Step-by-Step Guide

### Step 1: 'Check contents of plot_carpet for img with many volumes.'

```python
'Check contents of plot_carpet for img with many volumes.'
```

**Verification:**
```python
assert plotted_array.size == n_items
```

### Step 2: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots()
```

### Step 3: Assign display = plot_carpet(...)

```python
display = plot_carpet(img_4d_long_mni, img_3d_ones_mni, title='TEST', figure=fig, axes=ax, standardize='zscore_sample')
```

### Step 4: Assign ax = value

```python
ax = display.axes[0]
```

### Step 5: Assign plotted_array = unknown.get_array(...)

```python
plotted_array = ax.images[0].get_array()
```

### Step 6: Assign n_items = value

```python
n_items = np.prod(img_4d_long_mni.shape[:-1]) * np.ceil(img_4d_long_mni.shape[-1] / 2)
```

**Verification:**
```python
assert plotted_array.size == n_items
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, img_3d_ones_mni, img_4d_long_mni

# Workflow
'Check contents of plot_carpet for img with many volumes.'
fig, ax = plt.subplots()
display = plot_carpet(img_4d_long_mni, img_3d_ones_mni, title='TEST', figure=fig, axes=ax, standardize='zscore_sample')
ax = display.axes[0]
plotted_array = ax.images[0].get_array()
n_items = np.prod(img_4d_long_mni.shape[:-1]) * np.ceil(img_4d_long_mni.shape[-1] / 2)
assert plotted_array.size == n_items
```

## Next Steps


---

*Source: test_plot_carpet.py:37 | Complexity: Intermediate | Last updated: 2026-05-18*