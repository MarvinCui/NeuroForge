# How To: Plot Topomap Cnorm

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test colormap normalization.

## Prerequisites

**Required Modules:**
- `functools`
- `pathlib`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.patches`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.time_frequency.tfr`
- `mne.viz`
- `mne.viz.tests.test_raw`
- `mne.viz.topomap`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test colormap normalization.'

```python
'Test colormap normalization.'
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(42)
```

### Step 3: Assign v = rng.uniform(...)

```python
v = rng.uniform(low=-1, high=2.5, size=64)
```

### Step 4: Assign unknown = value

```python
v[:3] = [-1, 0, 2.5]
```

### Step 5: Assign montage = make_standard_montage(...)

```python
montage = make_standard_montage('biosemi64')
```

### Step 6: Assign info = create_info.set_montage(...)

```python
info = create_info(montage.ch_names, 256, 'eeg').set_montage('biosemi64')
```

### Step 7: Assign cnorm = TwoSlopeNorm(...)

```python
cnorm = TwoSlopeNorm(vmin=-1, vcenter=0, vmax=2.5)
```

### Step 8: Call plot_topomap()

```python
plot_topomap(v, info, cnorm=cnorm)
```

### Step 9: Call plot_topomap()

```python
plot_topomap(v, info, cnorm=PowerNorm(0.5))
```

### Step 10: Call plot_topomap()

```python
plot_topomap(v, info, vlim=(-10, None), cnorm=cnorm)
```

### Step 11: Call plot_topomap()

```python
plot_topomap(v, info, vlim=(None, 10), cnorm=cnorm)
```


## Complete Example

```python
# Workflow
'Test colormap normalization.'
rng = np.random.default_rng(42)
v = rng.uniform(low=-1, high=2.5, size=64)
v[:3] = [-1, 0, 2.5]
montage = make_standard_montage('biosemi64')
info = create_info(montage.ch_names, 256, 'eeg').set_montage('biosemi64')
cnorm = TwoSlopeNorm(vmin=-1, vcenter=0, vmax=2.5)
plot_topomap(v, info, cnorm=cnorm)
with pytest.warns(RuntimeWarning, match='implicitly defines vmin=-1'):
    plot_topomap(v, info, vlim=(-10, None), cnorm=cnorm)
with pytest.warns(RuntimeWarning, match='implicitly defines .* vmax=2.5'):
    plot_topomap(v, info, vlim=(None, 10), cnorm=cnorm)
plot_topomap(v, info, cnorm=PowerNorm(0.5))
```

## Next Steps


---

*Source: test_topomap.py:885 | Complexity: Advanced | Last updated: 2026-05-18*