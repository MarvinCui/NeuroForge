# How To: Plot Topomap Bads

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting topomap with bad channels (gh-7213).

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

### Step 1: 'Test plotting topomap with bad channels (gh-7213).'

```python
'Test plotting topomap with bad channels (gh-7213).'
```

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(3, 1000)
```

### Step 3: Assign raw = RawArray(...)

```python
raw = RawArray(data, create_info(3, 1000.0, 'eeg'))
```

### Step 4: Assign ch_pos_dict = value

```python
ch_pos_dict = {name: pos for name, pos in zip(raw.ch_names, np.eye(3))}
```

### Step 5: Call raw.info.set_montage()

```python
raw.info.set_montage(make_dig_montage(ch_pos_dict, coord_frame='head'))
```

### Step 6: Assign unknown = value

```python
raw.info['bads'] = raw.ch_names[:count]
```

### Step 7: Call raw.info._check_consistency()

```python
raw.info._check_consistency()
```

### Step 8: Call plot_topomap()

```python
plot_topomap(data[:, 0], raw.info)
```


## Complete Example

```python
# Workflow
'Test plotting topomap with bad channels (gh-7213).'
data = np.random.RandomState(0).randn(3, 1000)
raw = RawArray(data, create_info(3, 1000.0, 'eeg'))
ch_pos_dict = {name: pos for name, pos in zip(raw.ch_names, np.eye(3))}
raw.info.set_montage(make_dig_montage(ch_pos_dict, coord_frame='head'))
for count in range(3):
    raw.info['bads'] = raw.ch_names[:count]
    raw.info._check_consistency()
    plot_topomap(data[:, 0], raw.info)
```

## Next Steps


---

*Source: test_topomap.py:747 | Complexity: Advanced | Last updated: 2026-05-18*