# How To: Plot Topo Image Epochs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of epochs image topography.

## Prerequisites

**Required Modules:**
- `collections`
- `pathlib`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.viz`
- `mne.viz.evoked`
- `mne.viz.topo`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plotting of epochs image topography.'

```python
'Test plotting of epochs image topography.'
```

**Verification:**
```python
assert epochs._data.min() == data_min
```

### Step 2: Assign title = 'ERF images - MNE sample data'

```python
title = 'ERF images - MNE sample data'
```

**Verification:**
```python
assert num_figures_before + 1 == len(plt.get_fignums())
```

### Step 3: Assign epochs = _get_epochs(...)

```python
epochs = _get_epochs()
```

**Verification:**
```python
assert len(qm_cmap) >= 1
```

### Step 4: Call epochs.load_data()

```python
epochs.load_data()
```

**Verification:**
```python
assert qm_cmap[0] is cmap
```

### Step 5: Assign cmap = mne_analyze_colormap(...)

```python
cmap = mne_analyze_colormap(format='matplotlib')
```

### Step 6: Assign data_min = epochs._data.min(...)

```python
data_min = epochs._data.min()
```

### Step 7: Call plt.close()

```python
plt.close('all')
```

### Step 8: Assign fig = plot_topo_image_epochs(...)

```python
fig = plot_topo_image_epochs(epochs, sigma=0.5, vmin=-200, vmax=200, colorbar=True, title=title, cmap=cmap)
```

**Verification:**
```python
assert epochs._data.min() == data_min
```

### Step 9: Assign num_figures_before = len(...)

```python
num_figures_before = len(plt.get_fignums())
```

### Step 10: Call _fake_click()

```python
_fake_click(fig, fig.axes[0], (0.08, 0.64))
```

**Verification:**
```python
assert num_figures_before + 1 == len(plt.get_fignums())
```

### Step 11: Assign ep = epochs.copy.pick(...)

```python
ep = epochs.copy().pick(picks='eeg')
```

### Step 12: Assign fig = plot_topo_image_epochs(...)

```python
fig = plot_topo_image_epochs(ep, vmin=None, vmax=None, colorbar=None, cmap=cmap)
```

### Step 13: Assign ax = value

```python
ax = [x for x in fig.get_children() if isinstance(x, matplotlib.axes.Axes)]
```

### Step 14: Call ax.extend()

```python
ax.extend((y for x in ax for y in x.get_children() if isinstance(y, matplotlib.axes.Axes)))
```

### Step 15: Assign qm_cmap = value

```python
qm_cmap = [y.cmap for x in ax for y in x.get_children() if isinstance(y, matplotlib.collections.QuadMesh)]
```

**Verification:**
```python
assert len(qm_cmap) >= 1
```


## Complete Example

```python
# Workflow
'Test plotting of epochs image topography.'
title = 'ERF images - MNE sample data'
epochs = _get_epochs()
epochs.load_data()
cmap = mne_analyze_colormap(format='matplotlib')
data_min = epochs._data.min()
plt.close('all')
fig = plot_topo_image_epochs(epochs, sigma=0.5, vmin=-200, vmax=200, colorbar=True, title=title, cmap=cmap)
assert epochs._data.min() == data_min
num_figures_before = len(plt.get_fignums())
_fake_click(fig, fig.axes[0], (0.08, 0.64))
assert num_figures_before + 1 == len(plt.get_fignums())
ep = epochs.copy().pick(picks='eeg')
fig = plot_topo_image_epochs(ep, vmin=None, vmax=None, colorbar=None, cmap=cmap)
ax = [x for x in fig.get_children() if isinstance(x, matplotlib.axes.Axes)]
ax.extend((y for x in ax for y in x.get_children() if isinstance(y, matplotlib.axes.Axes)))
qm_cmap = [y.cmap for x in ax for y in x.get_children() if isinstance(y, matplotlib.collections.QuadMesh)]
assert len(qm_cmap) >= 1
assert qm_cmap[0] is cmap
```

## Next Steps


---

*Source: test_topo.py:292 | Complexity: Advanced | Last updated: 2026-05-18*