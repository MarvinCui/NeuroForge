# How To: Fnirs Channel Naming And Order Custom Optical Density

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Ensure fNIRS channel checking on manually created data.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`


## Step-by-Step Guide

### Step 1: 'Ensure fNIRS channel checking on manually created data.'

```python
'Ensure fNIRS channel checking on manually created data.'
```

**Verification:**
```python
assert len(picks) == len(raw.ch_names)
```

### Step 2: Assign data = np.random.normal(...)

```python
data = np.random.normal(size=(6, 10))
```

**Verification:**
```python
assert len(picks) == 6
```

### Step 3: Assign ch_names = value

```python
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D1 760', 'S2_D1 850', 'S3_D1 760', 'S3_D1 850']
```

### Step 4: Assign ch_types = np.repeat(...)

```python
ch_types = np.repeat('fnirs_od', 6)
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 7: Assign freqs = np.tile(...)

```python
freqs = np.tile([760, 850], 3)
```

### Step 8: Assign freqs = np.unique(...)

```python
freqs = np.unique(_channel_frequencies(raw.info))
```

### Step 9: Assign picks = _check_channels_ordered(...)

```python
picks = _check_channels_ordered(raw.info, freqs)
```

**Verification:**
```python
assert len(picks) == len(raw.ch_names)
```

### Step 10: Assign ch_names = value

```python
ch_names = ['S1_D1 760', 'S2_D1 760', 'S3_D1 760', 'S1_D1 850', 'S2_D1 850', 'S3_D1 850']
```

### Step 11: Assign ch_types = np.repeat(...)

```python
ch_types = np.repeat('fnirs_od', 6)
```

### Step 12: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 13: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 14: Assign freqs = np.repeat(...)

```python
freqs = np.repeat([760, 850], 3)
```

### Step 15: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, [760, 850])
```

### Step 16: Call raw.pick()

```python
raw.pick(picks=[0, 3, 1, 4, 2, 5])
```

### Step 17: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, [760, 850])
```

### Step 18: Assign ch_names = value

```python
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
```

### Step 19: Assign ch_types = np.tile(...)

```python
ch_types = np.tile(['hbo', 'hbr'], 3)
```

### Step 20: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 21: Assign raw2 = RawArray(...)

```python
raw2 = RawArray(data, info, verbose=True)
```

### Step 22: Call raw.add_channels()

```python
raw.add_channels([raw2])
```

### Step 23: Assign unknown = f

```python
raw.info['chs'][idx]['loc'][9] = f
```

### Step 24: Assign unknown = f

```python
raw.info['chs'][idx]['loc'][9] = f
```

### Step 25: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, [760, 850])
```


## Complete Example

```python
# Workflow
'Ensure fNIRS channel checking on manually created data.'
data = np.random.normal(size=(6, 10))
ch_names = ['S1_D1 760', 'S1_D1 850', 'S2_D1 760', 'S2_D1 850', 'S3_D1 760', 'S3_D1 850']
ch_types = np.repeat('fnirs_od', 6)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
freqs = np.tile([760, 850], 3)
for idx, f in enumerate(freqs):
    raw.info['chs'][idx]['loc'][9] = f
freqs = np.unique(_channel_frequencies(raw.info))
picks = _check_channels_ordered(raw.info, freqs)
assert len(picks) == len(raw.ch_names)
assert len(picks) == 6
ch_names = ['S1_D1 760', 'S2_D1 760', 'S3_D1 760', 'S1_D1 850', 'S2_D1 850', 'S3_D1 850']
ch_types = np.repeat('fnirs_od', 6)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
freqs = np.repeat([760, 850], 3)
for idx, f in enumerate(freqs):
    raw.info['chs'][idx]['loc'][9] = f
_check_channels_ordered(raw.info, [760, 850])
raw.pick(picks=[0, 3, 1, 4, 2, 5])
_check_channels_ordered(raw.info, [760, 850])
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw2 = RawArray(data, info, verbose=True)
raw.add_channels([raw2])
with pytest.raises(ValueError, match='does not support a combination'):
    _check_channels_ordered(raw.info, [760, 850])
```

## Next Steps


---

*Source: test_nirs.py:372 | Complexity: Advanced | Last updated: 2026-05-18*