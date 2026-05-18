# How To: 1020 Selection

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test making a 10/20 selection dict.

## Prerequisites

**Required Modules:**
- `hashlib`
- `contextlib`
- `copy`
- `functools`
- `pathlib`
- `numpy`
- `pooch`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.channels.channels`
- `mne.datasets`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test making a 10/20 selection dict.'

```python
'Test making a 10/20 selection dict.'
```

**Verification:**
```python
assert fs > ps
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pymatreader')
```

**Verification:**
```python
assert channel in sels[roi]
```

### Step 3: Assign raw_fname = value

```python
raw_fname = testing_path / 'EEGLAB' / 'test_raw.set'
```

**Verification:**
```python
assert ch_names == [raw.ch_names[idx] for idx in sels[selection]]
```

### Step 4: Assign loc_fname = value

```python
loc_fname = testing_path / 'EEGLAB' / 'test_chans.locs'
```

### Step 5: Assign raw = read_raw_eeglab(...)

```python
raw = read_raw_eeglab(raw_fname, preload=True)
```

### Step 6: Assign montage = read_custom_montage(...)

```python
montage = read_custom_montage(loc_fname)
```

### Step 7: Assign raw = raw.rename_channels(...)

```python
raw = raw.rename_channels(dict(zip(raw.ch_names, montage.ch_names)))
```

### Step 8: Call raw.set_montage()

```python
raw.set_montage(montage)
```

### Step 9: Assign sels = make_1020_channel_selections(...)

```python
sels = make_1020_channel_selections(raw.info)
```

### Step 10: Assign fz_c3_c4 = value

```python
fz_c3_c4 = [raw.ch_names.index(ch) for ch in ('Fz', 'C3', 'C4')]
```

### Step 11: Assign sels_names = make_1020_channel_selections(...)

```python
sels_names = make_1020_channel_selections(raw.info, return_ch_names=True)
```

### Step 12: Call pytest.raises()

```python
pytest.raises(TypeError, make_1020_channel_selections, input_)
```

### Step 13: Assign fs = min(...)

```python
fs = min([ii for ii, pick in enumerate(picks) if raw.ch_names[pick].startswith('F')])
```

### Step 14: Assign ps = max(...)

```python
ps = max([ii for ii, pick in enumerate(picks) if raw.ch_names[pick].startswith('O')])
```

**Verification:**
```python
assert fs > ps
```


## Complete Example

```python
# Workflow
'Test making a 10/20 selection dict.'
pytest.importorskip('pymatreader')
raw_fname = testing_path / 'EEGLAB' / 'test_raw.set'
loc_fname = testing_path / 'EEGLAB' / 'test_chans.locs'
raw = read_raw_eeglab(raw_fname, preload=True)
montage = read_custom_montage(loc_fname)
raw = raw.rename_channels(dict(zip(raw.ch_names, montage.ch_names)))
raw.set_montage(montage)
for input_ in ('a_string', 100, raw, [1, 2]):
    pytest.raises(TypeError, make_1020_channel_selections, input_)
sels = make_1020_channel_selections(raw.info)
for name, picks in sels.items():
    fs = min([ii for ii, pick in enumerate(picks) if raw.ch_names[pick].startswith('F')])
    ps = max([ii for ii, pick in enumerate(picks) if raw.ch_names[pick].startswith('O')])
    assert fs > ps
fz_c3_c4 = [raw.ch_names.index(ch) for ch in ('Fz', 'C3', 'C4')]
for channel, roi in zip(fz_c3_c4, ('Midline', 'Left', 'Right')):
    assert channel in sels[roi]
sels_names = make_1020_channel_selections(raw.info, return_ch_names=True)
for selection, ch_names in sels_names.items():
    assert ch_names == [raw.ch_names[idx] for idx in sels[selection]]
```

## Next Steps


---

*Source: test_channels.py:403 | Complexity: Advanced | Last updated: 2026-05-18*