# How To: Plot Topo Single Ch

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test single channel topoplot with time cursor.

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

### Step 1: 'Test single channel topoplot with time cursor.'

```python
'Test single channel topoplot with time cursor.'
```

**Verification:**
```python
assert 'MEG 0113' in ax.format_coord(0.065, 0.63)
```

### Step 2: Assign evoked = _get_epochs.average(...)

```python
evoked = _get_epochs().average()
```

**Verification:**
```python
assert num_figures_before + 1 == len(plt.get_fignums())
```

### Step 3: Assign evoked2 = evoked.copy(...)

```python
evoked2 = evoked.copy()
```

**Verification:**
```python
assert isinstance(ax._cursorline, matplotlib.lines.Line2D)
```

### Step 4: Call evoked.crop()

```python
evoked.crop(-0.19, 0)
```

**Verification:**
```python
assert ax._cursorline is None
```

### Step 5: Call evoked2.crop()

```python
evoked2.crop(0.05, 0.19)
```

### Step 6: Assign fig = plot_evoked_topo(...)

```python
fig = plot_evoked_topo([evoked, evoked2], background_color='w')
```

### Step 7: Assign ax = plt.gca(...)

```python
ax = plt.gca()
```

**Verification:**
```python
assert 'MEG 0113' in ax.format_coord(0.065, 0.63)
```

### Step 8: Assign num_figures_before = len(...)

```python
num_figures_before = len(plt.get_fignums())
```

### Step 9: Call _fake_click()

```python
_fake_click(fig, fig.axes[0], (0.08, 0.65))
```

**Verification:**
```python
assert num_figures_before + 1 == len(plt.get_fignums())
```

### Step 10: Assign fig = plt.gcf(...)

```python
fig = plt.gcf()
```

### Step 11: Assign ax = plt.gca(...)

```python
ax = plt.gca()
```

### Step 12: Call _fake_click()

```python
_fake_click(fig, ax, (0.5, 0.5), kind='motion')
```

**Verification:**
```python
assert isinstance(ax._cursorline, matplotlib.lines.Line2D)
```

### Step 13: Call _fake_click()

```python
_fake_click(fig, ax, (1.5, 1.5), kind='motion')
```

**Verification:**
```python
assert ax._cursorline is None
```

### Step 14: Call plt.close()

```python
plt.close('all')
```


## Complete Example

```python
# Workflow
'Test single channel topoplot with time cursor.'
evoked = _get_epochs().average()
evoked2 = evoked.copy()
evoked.crop(-0.19, 0)
evoked2.crop(0.05, 0.19)
fig = plot_evoked_topo([evoked, evoked2], background_color='w')
ax = plt.gca()
assert 'MEG 0113' in ax.format_coord(0.065, 0.63)
num_figures_before = len(plt.get_fignums())
_fake_click(fig, fig.axes[0], (0.08, 0.65))
assert num_figures_before + 1 == len(plt.get_fignums())
fig = plt.gcf()
ax = plt.gca()
_fake_click(fig, ax, (0.5, 0.5), kind='motion')
assert isinstance(ax._cursorline, matplotlib.lines.Line2D)
_fake_click(fig, ax, (1.5, 1.5), kind='motion')
assert ax._cursorline is None
plt.close('all')
```

## Next Steps


---

*Source: test_topo.py:269 | Complexity: Advanced | Last updated: 2026-05-18*