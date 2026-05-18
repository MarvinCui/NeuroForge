# How To: Plot Psd Epochs Ctf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting CTF epochs psd (+topomap).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.utils`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: raw_ctf
```

## Step-by-Step Guide

### Step 1: 'Test plotting CTF epochs psd (+topomap).'

```python
'Test plotting CTF epochs psd (+topomap).'
```

### Step 2: Assign evts = make_fixed_length_events(...)

```python
evts = make_fixed_length_events(raw_ctf)
```

### Step 3: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw_ctf, evts, preload=True)
```

### Step 4: Assign old_defaults = dict(...)

```python
old_defaults = dict(picks='data', exclude='bads')
```

### Step 5: Call spectrum.drop_channels()

```python
spectrum.drop_channels(['EEG060'])
```

### Step 6: Call spectrum.plot()

```python
spectrum.plot(spatial_colors=False, average=False, amplitude=False, **old_defaults)
```

### Step 7: Call spectrum.plot_topomap()

```python
spectrum.plot_topomap()
```

### Step 8: Assign spectrum = epochs.compute_psd(...)

```python
spectrum = epochs.compute_psd()
```

### Step 9: Call spectrum.plot_topomap()

```python
spectrum.plot_topomap(bands=[(0, 0.01, 'foo')])
```

### Step 10: Call spectrum.plot()

```python
spectrum.plot(dB=dB)
```


## Complete Example

```python
# Setup
# Fixtures: raw_ctf

# Workflow
'Test plotting CTF epochs psd (+topomap).'
evts = make_fixed_length_events(raw_ctf)
epochs = Epochs(raw_ctf, evts, preload=True)
old_defaults = dict(picks='data', exclude='bads')
with _record_warnings(), pytest.warns(UserWarning, match='for channel EEG060'):
    spectrum = epochs.compute_psd()
    for dB in [True, False]:
        spectrum.plot(dB=dB)
spectrum.drop_channels(['EEG060'])
spectrum.plot(spatial_colors=False, average=False, amplitude=False, **old_defaults)
with pytest.raises(RuntimeError, match='No frequencies in band'):
    spectrum.plot_topomap(bands=[(0, 0.01, 'foo')])
spectrum.plot_topomap()
```

## Next Steps


---

*Source: test_epochs.py:491 | Complexity: Advanced | Last updated: 2026-05-18*