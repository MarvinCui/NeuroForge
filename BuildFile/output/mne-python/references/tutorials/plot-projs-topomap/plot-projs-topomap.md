# How To: Plot Projs Topomap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_projs_topomap.

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

### Step 1: 'Test plot_projs_topomap.'

```python
'Test plot_projs_topomap.'
```

### Step 2: Assign projs = read_proj(...)

```python
projs = read_proj(ecg_fname)
```

### Step 3: Assign info = read_info(...)

```python
info = read_info(raw_fname)
```

### Step 4: Call plot_projs_topomap()

```python
plot_projs_topomap(projs, info=info, colorbar=True, **fast_test)
```

### Step 5: Assign unknown = plt.subplots(...)

```python
_, ax = plt.subplots()
```

### Step 6: Call unknown.plot_topomap()

```python
projs[3].plot_topomap(info)
```

### Step 7: Call plot_projs_topomap()

```python
plot_projs_topomap(projs[:1], info, axes=ax, **fast_test)
```

### Step 8: Assign triux_info = read_info(...)

```python
triux_info = read_info(triux_fname)
```

### Step 9: Call plot_projs_topomap()

```python
plot_projs_topomap(triux_info['projs'][-1:], triux_info, **fast_test)
```

### Step 10: Call plot_projs_topomap()

```python
plot_projs_topomap(triux_info['projs'][:1], triux_info, **fast_test)
```

### Step 11: Assign eeg_avg = make_eeg_average_ref_proj(...)

```python
eeg_avg = make_eeg_average_ref_proj(info)
```

### Step 12: Call eeg_avg.plot_topomap()

```python
eeg_avg.plot_topomap(info, **fast_test)
```

### Step 13: Assign eeg_proj = make_eeg_average_ref_proj(...)

```python
eeg_proj = make_eeg_average_ref_proj(info)
```

### Step 14: Assign info_meg = pick_info(...)

```python
info_meg = pick_info(info, pick_types(info, meg=True, eeg=False))
```

### Step 15: Call plot_projs_topomap()

```python
plot_projs_topomap(projs[:-1], info, vlim=vlim, colorbar=True)
```

### Step 16: Call plot_projs_topomap()

```python
plot_projs_topomap([eeg_proj], info_meg)
```


## Complete Example

```python
# Workflow
'Test plot_projs_topomap.'
projs = read_proj(ecg_fname)
info = read_info(raw_fname)
plot_projs_topomap(projs, info=info, colorbar=True, **fast_test)
_, ax = plt.subplots()
projs[3].plot_topomap(info)
plot_projs_topomap(projs[:1], info, axes=ax, **fast_test)
triux_info = read_info(triux_fname)
plot_projs_topomap(triux_info['projs'][-1:], triux_info, **fast_test)
plot_projs_topomap(triux_info['projs'][:1], triux_info, **fast_test)
eeg_avg = make_eeg_average_ref_proj(info)
eeg_avg.plot_topomap(info, **fast_test)
for vlim in ('joint', (-1, 1), (None, 0.5), (0.5, None), (None, None)):
    plot_projs_topomap(projs[:-1], info, vlim=vlim, colorbar=True)
eeg_proj = make_eeg_average_ref_proj(info)
info_meg = pick_info(info, pick_types(info, meg=True, eeg=False))
with pytest.raises(ValueError, match='Missing channels'):
    plot_projs_topomap([eeg_proj], info_meg)
```

## Next Steps


---

*Source: test_topomap.py:138 | Complexity: Advanced | Last updated: 2026-05-18*