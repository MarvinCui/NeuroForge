# How To: Plot Alignment Ieeg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting of iEEG sensors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.figure`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.defaults`
- `mne.fixes`
- `mne.io`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`
- `mne.viz`
- `mne.viz._3d`
- `mne.viz.utils`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: renderer, test_ecog, test_seeg, sensor_colors, sensor_scales, expectation
```

## Step-by-Step Guide

### Step 1: 'Test plotting of iEEG sensors.'

```python
'Test plotting of iEEG sensors.'
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 2: Assign evoked = value

```python
evoked = read_evokeds(evoked_fname)[0]
```

### Step 3: Assign evoked_eeg = evoked.copy.pick_types(...)

```python
evoked_eeg = evoked.copy().pick_types(eeg=True)
```

### Step 4: Assign eeg_channels = pick_types(...)

```python
eeg_channels = pick_types(evoked_eeg.info, eeg=True)
```

### Step 5: Call evoked_eeg.set_channel_types()

```python
evoked_eeg.set_channel_types({evoked_eeg.ch_names[ch]: 'ecog' for ch in eeg_channels[:10]})
```

### Step 6: Call evoked_eeg.set_channel_types()

```python
evoked_eeg.set_channel_types({evoked_eeg.ch_names[ch]: 'seeg' for ch in eeg_channels[10:20]})
```

### Step 7: Assign evoked_ecog_seeg = evoked_eeg.pick_types(...)

```python
evoked_ecog_seeg = evoked_eeg.pick_types(seeg=True, ecog=True)
```

### Step 8: Assign this_info = value

```python
this_info = evoked_ecog_seeg.info
```

### Step 9: Assign unknown = value

```python
evoked_eeg.info['projs'] = []
```

### Step 10: Assign fig = plot_alignment(...)

```python
fig = plot_alignment(this_info, ecog=test_ecog, seeg=test_seeg, sensor_colors=sensor_colors, sensor_scales=sensor_scales)
```

**Verification:**
```python
assert isinstance(fig, Figure3D)
```

### Step 11: Call renderer.backend._close_all()

```python
renderer.backend._close_all()
```


## Complete Example

```python
# Setup
# Fixtures: renderer, test_ecog, test_seeg, sensor_colors, sensor_scales, expectation

# Workflow
'Test plotting of iEEG sensors.'
evoked = read_evokeds(evoked_fname)[0]
evoked_eeg = evoked.copy().pick_types(eeg=True)
with evoked_eeg.info._unlock():
    evoked_eeg.info['projs'] = []
eeg_channels = pick_types(evoked_eeg.info, eeg=True)
evoked_eeg.set_channel_types({evoked_eeg.ch_names[ch]: 'ecog' for ch in eeg_channels[:10]})
evoked_eeg.set_channel_types({evoked_eeg.ch_names[ch]: 'seeg' for ch in eeg_channels[10:20]})
evoked_ecog_seeg = evoked_eeg.pick_types(seeg=True, ecog=True)
this_info = evoked_ecog_seeg.info
with expectation:
    fig = plot_alignment(this_info, ecog=test_ecog, seeg=test_seeg, sensor_colors=sensor_colors, sensor_scales=sensor_scales)
    assert isinstance(fig, Figure3D)
    renderer.backend._close_all()
```

## Next Steps


---

*Source: test_3d.py:411 | Complexity: Advanced | Last updated: 2026-05-18*