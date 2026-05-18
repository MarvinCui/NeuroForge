# How To: Interpolation Nirs Reordered Picks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test NIRS interpolation uses the closest donor in raw channel space.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.channels`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne.channels`
- `mne.channels.interpolation`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`
- `mne.channels.interpolation`


## Step-by-Step Guide

### Step 1: 'Test NIRS interpolation uses the closest donor in raw channel space.'

```python
'Test NIRS interpolation uses the closest donor in raw channel space.'
```

**Verification:**
```python
assert_allclose(raw.get_data(picks=picks_bad), raw.get_data(picks=picks_want))
```

### Step 2: Assign ch_names = value

```python
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850', 'S3_D3 760', 'S3_D3 850', 'S10_D10 760', 'S10_D10 850']
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=1.0, ch_types=['fnirs_cw_amplitude'] * 8)
```

### Step 4: Assign pair_positions = value

```python
pair_positions = {'S1_D1': (0.009, 0.0, 0.0), 'S2_D2': (0.01, 0.0, 0.0), 'S3_D3': (0.03, 0.0, 0.0), 'S10_D10': (0.04, 0.0, 0.0)}
```

### Step 5: Assign data = np.arange.reshape(...)

```python
data = np.arange(len(ch_names), dtype=float).reshape(-1, 1)
```

### Step 6: Assign data = np.repeat(...)

```python
data = np.repeat(data, 5, axis=1)
```

### Step 7: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=False)
```

### Step 8: Assign unknown = value

```python
raw.info['bads'] = ['S2_D2 760', 'S2_D2 850']
```

### Step 9: Call raw.interpolate_bads()

```python
raw.interpolate_bads(method=dict(fnirs='nearest'), origin=(0.0, 0.0, 0.0), verbose=False)
```

### Step 10: Assign picks_bad = pick_channels(...)

```python
picks_bad = pick_channels(raw.ch_names, ['S2_D2 760', 'S2_D2 850'], exclude=[])
```

### Step 11: Assign picks_want = pick_channels(...)

```python
picks_want = pick_channels(raw.ch_names, ['S1_D1 760', 'S1_D1 850'], exclude=[])
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw.get_data(picks=picks_bad), raw.get_data(picks=picks_want))
```

### Step 13: Assign pair = value

```python
pair = ch['ch_name'].rsplit(' ', 1)[0]
```

### Step 14: Assign unknown = value

```python
ch['loc'][:3] = pair_positions[pair]
```

### Step 15: Assign unknown = value

```python
ch['loc'][9] = 760.0 if idx % 2 == 0 else 850.0
```


## Complete Example

```python
# Workflow
'Test NIRS interpolation uses the closest donor in raw channel space.'
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850', 'S3_D3 760', 'S3_D3 850', 'S10_D10 760', 'S10_D10 850']
info = create_info(ch_names, sfreq=1.0, ch_types=['fnirs_cw_amplitude'] * 8)
pair_positions = {'S1_D1': (0.009, 0.0, 0.0), 'S2_D2': (0.01, 0.0, 0.0), 'S3_D3': (0.03, 0.0, 0.0), 'S10_D10': (0.04, 0.0, 0.0)}
for idx, ch in enumerate(info['chs']):
    pair = ch['ch_name'].rsplit(' ', 1)[0]
    ch['loc'][:3] = pair_positions[pair]
    ch['loc'][9] = 760.0 if idx % 2 == 0 else 850.0
data = np.arange(len(ch_names), dtype=float).reshape(-1, 1)
data = np.repeat(data, 5, axis=1)
raw = RawArray(data, info, verbose=False)
raw.info['bads'] = ['S2_D2 760', 'S2_D2 850']
raw.interpolate_bads(method=dict(fnirs='nearest'), origin=(0.0, 0.0, 0.0), verbose=False)
picks_bad = pick_channels(raw.ch_names, ['S2_D2 760', 'S2_D2 850'], exclude=[])
picks_want = pick_channels(raw.ch_names, ['S1_D1 760', 'S1_D1 850'], exclude=[])
assert_allclose(raw.get_data(picks=picks_bad), raw.get_data(picks=picks_want))
```

## Next Steps


---

*Source: test_interpolation.py:336 | Complexity: Advanced | Last updated: 2026-05-18*