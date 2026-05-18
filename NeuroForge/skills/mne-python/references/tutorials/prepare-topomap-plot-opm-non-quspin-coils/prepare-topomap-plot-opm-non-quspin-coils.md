# How To: Prepare Topomap Plot Opm Non Quspin Coils

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test colocated OPM handling for non-QuSpin OPM coil types.

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

### Step 1: 'Test colocated OPM handling for non-QuSpin OPM coil types.'

```python
'Test colocated OPM handling for non-QuSpin OPM coil types.'
```

**Verification:**
```python
assert len(picks) == 6
```

### Step 2: Assign ch_names = value

```python
ch_names = ['OPM001', 'OPM002', 'OPM003', 'OPM004', 'OPM005', 'OPM006']
```

**Verification:**
```python
assert merge_channels
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names, 1000.0, ch_types='mag')
```

**Verification:**
```python
assert len(merge_channels) == 2
```

### Step 4: Assign positions = np.array(...)

```python
positions = np.array([[0.03, 0.0, 0.05], [0.03, 0.0, 0.05], [0.03, 0.0, 0.05], [-0.03, 0.0, 0.05], [-0.03, 0.0, 0.05], [-0.03, 0.0, 0.05]])
```

**Verification:**
```python
assert all((len(set_) == 3 for set_ in merge_channels))
```

### Step 5: Assign orientations = np.array(...)

```python
orientations = np.array([[0.5145, 0.0, 0.8575], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0], [-0.5145, 0.0, 0.8575], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0]])
```

**Verification:**
```python
assert sum((name.endswith('MERGE-REMOVE') for name in merged_names)) == 4
```

### Step 6: Assign evoked = EvokedArray(...)

```python
evoked = EvokedArray(np.zeros((len(ch_names), 5)), info)
```

### Step 7: Assign unknown = topomap._prepare_topomap_plot(...)

```python
picks, _pos, merge_channels, merged_names, *_ = topomap._prepare_topomap_plot(evoked, 'mag')
```

**Verification:**
```python
assert len(picks) == 6
```

### Step 8: Assign unknown = value

```python
ch['coil_type'] = FIFF.FIFFV_COIL_FIELDLINE_OPM_MAG_GEN1
```

### Step 9: Assign unknown = value

```python
ch['loc'][:3] = positions[idx]
```

### Step 10: Assign unknown = value

```python
ch['loc'][9:12] = orientations[idx]
```


## Complete Example

```python
# Workflow
'Test colocated OPM handling for non-QuSpin OPM coil types.'
ch_names = ['OPM001', 'OPM002', 'OPM003', 'OPM004', 'OPM005', 'OPM006']
info = create_info(ch_names, 1000.0, ch_types='mag')
positions = np.array([[0.03, 0.0, 0.05], [0.03, 0.0, 0.05], [0.03, 0.0, 0.05], [-0.03, 0.0, 0.05], [-0.03, 0.0, 0.05], [-0.03, 0.0, 0.05]])
orientations = np.array([[0.5145, 0.0, 0.8575], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0], [-0.5145, 0.0, 0.8575], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0]])
with info._unlock():
    for idx, ch in enumerate(info['chs']):
        ch['coil_type'] = FIFF.FIFFV_COIL_FIELDLINE_OPM_MAG_GEN1
        ch['loc'][:3] = positions[idx]
        ch['loc'][9:12] = orientations[idx]
evoked = EvokedArray(np.zeros((len(ch_names), 5)), info)
picks, _pos, merge_channels, merged_names, *_ = topomap._prepare_topomap_plot(evoked, 'mag')
assert len(picks) == 6
assert merge_channels
assert len(merge_channels) == 2
assert all((len(set_) == 3 for set_ in merge_channels))
assert sum((name.endswith('MERGE-REMOVE') for name in merged_names)) == 4
```

## Next Steps


---

*Source: test_topomap.py:800 | Complexity: Advanced | Last updated: 2026-05-18*