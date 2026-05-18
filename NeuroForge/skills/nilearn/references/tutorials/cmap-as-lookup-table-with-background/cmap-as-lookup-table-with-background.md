# How To: Cmap As Lookup Table With Background

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Ensure that the background color is dropped from lut.

regression test for https://github.com/nilearn/nilearn/issues/5934

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
# Fixtures: background_label
```

## Step-by-Step Guide

### Step 1: 'Ensure that the background color is dropped from lut.\n\n    regression test for https://github.com/nilearn/nilearn/issues/5934\n    '

```python
'Ensure that the background color is dropped from lut.\n\n    regression test for https://github.com/nilearn/nilearn/issues/5934\n    '
```

**Verification:**
```python
assert n_regions + 2 == fig._cbar.cmap.N
```

### Step 2: Assign n_regions = 7

```python
n_regions = 7
```

**Verification:**
```python
assert n_regions + 1 == fig._cbar.cmap.N
```

### Step 3: Assign label_img = _img_labels(...)

```python
label_img = _img_labels(n_regions=n_regions)
```

### Step 4: Assign lut = generate_atlas_look_up_table(...)

```python
lut = generate_atlas_look_up_table(index=label_img, background_label=background_label)
```

### Step 5: Assign color = value

```python
color = ['#000000', '#781286', '#4682b4', '#00760e', '#c43afa', '#dcf8a4', '#e69422', '#cd3e4e']
```

### Step 6: Assign unknown = color

```python
lut['color'] = color
```

### Step 7: Assign fig = plot_roi(...)

```python
fig = plot_roi(label_img, cmap=lut)
```

**Verification:**
```python
assert n_regions + 2 == fig._cbar.cmap.N
```


## Complete Example

```python
# Setup
# Fixtures: background_label

# Workflow
'Ensure that the background color is dropped from lut.\n\n    regression test for https://github.com/nilearn/nilearn/issues/5934\n    '
n_regions = 7
label_img = _img_labels(n_regions=n_regions)
lut = generate_atlas_look_up_table(index=label_img, background_label=background_label)
color = ['#000000', '#781286', '#4682b4', '#00760e', '#c43afa', '#dcf8a4', '#e69422', '#cd3e4e']
lut['color'] = color
fig = plot_roi(label_img, cmap=lut)
if background_label is None:
    assert n_regions + 2 == fig._cbar.cmap.N
else:
    assert n_regions + 1 == fig._cbar.cmap.N
```

## Next Steps


---

*Source: test_plot_roi.py:132 | Complexity: Intermediate | Last updated: 2026-05-18*