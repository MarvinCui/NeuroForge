# How To: Plot Psds Topomap Colorbar

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_psds_topomap colorbar option.

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

### Step 1: 'Test plot_psds_topomap colorbar option.'

```python
'Test plot_psds_topomap colorbar option.'
```

**Verification:**
```python
assert len(fig_cbar.axes) == 2
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert len(fig_nocbar.axes) == 1
```

### Step 3: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg='grad')
```

### Step 4: Assign info = pick_info(...)

```python
info = pick_info(raw.info, picks)
```

### Step 5: Assign freqs = np.arange(...)

```python
freqs = np.arange(3.0, 9.5)
```

### Step 6: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(42)
```

### Step 7: Assign psd = np.abs(...)

```python
psd = np.abs(rng.standard_normal((len(picks), len(freqs))))
```

### Step 8: Assign bands = value

```python
bands = {'theta': [4, 8]}
```

### Step 9: Call plt.close()

```python
plt.close('all')
```

### Step 10: Assign fig_cbar = plot_psds_topomap(...)

```python
fig_cbar = plot_psds_topomap(psd, freqs, info, colorbar=True, bands=bands)
```

**Verification:**
```python
assert len(fig_cbar.axes) == 2
```

### Step 11: Assign fig_nocbar = plot_psds_topomap(...)

```python
fig_nocbar = plot_psds_topomap(psd, freqs, info, colorbar=False, bands=bands)
```

**Verification:**
```python
assert len(fig_nocbar.axes) == 1
```


## Complete Example

```python
# Workflow
'Test plot_psds_topomap colorbar option.'
raw = read_raw_fif(raw_fname)
picks = pick_types(raw.info, meg='grad')
info = pick_info(raw.info, picks)
freqs = np.arange(3.0, 9.5)
rng = np.random.default_rng(42)
psd = np.abs(rng.standard_normal((len(picks), len(freqs))))
bands = {'theta': [4, 8]}
plt.close('all')
fig_cbar = plot_psds_topomap(psd, freqs, info, colorbar=True, bands=bands)
assert len(fig_cbar.axes) == 2
fig_nocbar = plot_psds_topomap(psd, freqs, info, colorbar=False, bands=bands)
assert len(fig_nocbar.axes) == 1
```

## Next Steps


---

*Source: test_topomap.py:579 | Complexity: Advanced | Last updated: 2026-05-18*