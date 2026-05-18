# How To: Plot Carpet With Atlas And Labels

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_carpet when using an atlas and labels.

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

### Step 1: 'Test plot_carpet when using an atlas and labels.'

```python
'Test plot_carpet when using an atlas and labels.'
```

**Verification:**
```python
assert len(display.axes) == 2
```

### Step 2: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots()
```

**Verification:**
```python
assert set(yticklabels) == set(img_atlas['labels'].keys())
```

### Step 3: Assign display = plot_carpet(...)

```python
display = plot_carpet(img_4d_mni, mask_img=img_atlas['img'], mask_labels=img_atlas['labels'], detrend=True, title='TEST', figure=fig, axes=ax, standardize='zscore_sample')
```

**Verification:**
```python
assert len(np.unique(colorbar)) == len(img_atlas['labels'])
```

### Step 4: Assign ax = value

```python
ax = display.axes[0]
```

### Step 5: Assign yticklabels = ax.get_yticklabels(...)

```python
yticklabels = ax.get_yticklabels()
```

### Step 6: Assign yticklabels = value

```python
yticklabels = [yt.get_text() for yt in yticklabels]
```

**Verification:**
```python
assert set(yticklabels) == set(img_atlas['labels'].keys())
```

### Step 7: Assign ax = value

```python
ax = display.axes[0]
```

### Step 8: Assign colorbar = unknown.get_array(...)

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
'Test plot_carpet when using an atlas and labels.'
fig, ax = plt.subplots()
display = plot_carpet(img_4d_mni, mask_img=img_atlas['img'], mask_labels=img_atlas['labels'], detrend=True, title='TEST', figure=fig, axes=ax, standardize='zscore_sample')
assert len(display.axes) == 2
ax = display.axes[0]
yticklabels = ax.get_yticklabels()
yticklabels = [yt.get_text() for yt in yticklabels]
assert set(yticklabels) == set(img_atlas['labels'].keys())
ax = display.axes[0]
colorbar = ax.images[0].get_array()
assert len(np.unique(colorbar)) == len(img_atlas['labels'])
```

## Next Steps


---

*Source: test_plot_carpet.py:90 | Complexity: Advanced | Last updated: 2026-05-18*