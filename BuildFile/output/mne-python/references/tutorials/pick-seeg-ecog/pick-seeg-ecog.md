# How To: Pick Seeg Ecog

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test picking with sEEG and ECoG.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test picking with sEEG and ECoG.'

```python
'Test picking with sEEG and ECoG.'
```

**Verification:**
```python
assert_indexing(info, picks_by_type)
```

### Step 2: Assign names = unknown.split(...)

```python
names = 'A1 A2 Fz O OTp1 OTp2 E1 OTp3 E2 E3'.split()
```

**Verification:**
```python
assert_array_equal(pick_types(info, meg=False, seeg=True), [4, 5, 7])
```

### Step 3: Assign types = unknown.split(...)

```python
types = 'mag mag eeg eeg seeg seeg ecog seeg ecog ecog'.split()
```

**Verification:**
```python
assert channel_type(info, i) == types[i]
```

### Step 4: Assign info = create_info(...)

```python
info = create_info(names, 1024.0, types)
```

**Verification:**
```python
assert lt == rt
```

### Step 5: Assign picks_by_type = value

```python
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('seeg', [4, 5, 7]), ('ecog', [6, 8, 9])]
```

**Verification:**
```python
assert len(pick_types(raw.info, meg=False, seeg=True, ecog=True)) == 0
```

### Step 6: Call assert_indexing()

```python
assert_indexing(info, picks_by_type)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(pick_types(info, meg=False, seeg=True), [4, 5, 7])
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((len(names), 10)), info)
```

### Step 9: Assign events = np.array(...)

```python
events = np.array([[1, 0, 0], [2, 0, 0]])
```

### Step 10: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events=events, event_id={'event': 0}, tmin=-1e-05, tmax=1e-05, baseline=(0, 0))
```

### Step 11: Assign evoked = epochs.average(...)

```python
evoked = epochs.average(pick_types(epochs.info, meg=True, seeg=True))
```

### Step 12: Assign e_seeg = evoked.copy.pick(...)

```python
e_seeg = evoked.copy().pick(picks='seeg')
```

### Step 13: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(io_dir / 'tests' / 'data' / 'test_chpi_raw_sss.fif')
```

**Verification:**
```python
assert len(pick_types(raw.info, meg=False, seeg=True, ecog=True)) == 0
```


## Complete Example

```python
# Workflow
'Test picking with sEEG and ECoG.'
names = 'A1 A2 Fz O OTp1 OTp2 E1 OTp3 E2 E3'.split()
types = 'mag mag eeg eeg seeg seeg ecog seeg ecog ecog'.split()
info = create_info(names, 1024.0, types)
picks_by_type = [('mag', [0, 1]), ('eeg', [2, 3]), ('seeg', [4, 5, 7]), ('ecog', [6, 8, 9])]
assert_indexing(info, picks_by_type)
assert_array_equal(pick_types(info, meg=False, seeg=True), [4, 5, 7])
for i, t in enumerate(types):
    assert channel_type(info, i) == types[i]
raw = RawArray(np.zeros((len(names), 10)), info)
events = np.array([[1, 0, 0], [2, 0, 0]])
epochs = Epochs(raw, events=events, event_id={'event': 0}, tmin=-1e-05, tmax=1e-05, baseline=(0, 0))
evoked = epochs.average(pick_types(epochs.info, meg=True, seeg=True))
e_seeg = evoked.copy().pick(picks='seeg')
for lt, rt in zip(e_seeg.ch_names, [names[4], names[5], names[7]]):
    assert lt == rt
raw = read_raw_fif(io_dir / 'tests' / 'data' / 'test_chpi_raw_sss.fif')
assert len(pick_types(raw.info, meg=False, seeg=True, ecog=True)) == 0
```

## Next Steps


---

*Source: test_pick.py:291 | Complexity: Advanced | Last updated: 2026-05-18*