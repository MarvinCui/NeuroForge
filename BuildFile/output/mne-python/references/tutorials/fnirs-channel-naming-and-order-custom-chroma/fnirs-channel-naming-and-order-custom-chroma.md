# How To: Fnirs Channel Naming And Order Custom Chroma

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

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(6, 10)
```

**Verification:**
```python
assert len(picks) == 6
```

### Step 3: Assign ch_names = value

```python
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
```

### Step 4: Assign ch_types = np.tile(...)

```python
ch_types = np.tile(['hbo', 'hbr'], 3)
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 7: Assign chroma = np.unique(...)

```python
chroma = np.unique(_channel_chromophore(raw.info))
```

### Step 8: Assign picks = _check_channels_ordered(...)

```python
picks = _check_channels_ordered(raw.info, chroma)
```

**Verification:**
```python
assert len(picks) == len(raw.ch_names)
```

### Step 9: Assign ch_names = value

```python
ch_names = ['S1_D1 hbo', 'S2_D1 hbo', 'S3_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbr', 'S3_D1 hbr']
```

### Step 10: Assign ch_types = np.repeat(...)

```python
ch_types = np.repeat(['hbo', 'hbr'], 3)
```

### Step 11: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 12: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 13: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
```

### Step 14: Call raw.pick()

```python
raw.pick(picks=[0, 3, 1, 4, 2, 5])
```

### Step 15: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
```

### Step 16: Assign ch_names = value

```python
ch_names = ['S1_D1 hbb', 'S1_D1 hbr', 'S2_D1 hbb', 'S2_D1 hbr', 'S3_D1 hbb', 'S3_D1 hbr']
```

### Step 17: Assign ch_types = np.tile(...)

```python
ch_types = np.tile(['hbo', 'hbr'], 3)
```

### Step 18: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 19: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 20: Assign ch_names = value

```python
ch_names = ['S1_DX hbo', 'S1_DX hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
```

### Step 21: Assign ch_types = np.tile(...)

```python
ch_types = np.tile(['hbo', 'hbr'], 3)
```

### Step 22: Assign info = create_info(...)

```python
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
```

### Step 23: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, verbose=True)
```

### Step 24: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, ['hbb', 'hbr'])
```

### Step 25: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
```

### Step 26: Call _check_channels_ordered()

```python
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
```


## Complete Example

```python
# Workflow
'Ensure fNIRS channel checking on manually created data.'
data = np.random.RandomState(0).randn(6, 10)
ch_names = ['S1_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
chroma = np.unique(_channel_chromophore(raw.info))
picks = _check_channels_ordered(raw.info, chroma)
assert len(picks) == len(raw.ch_names)
assert len(picks) == 6
ch_names = ['S1_D1 hbo', 'S2_D1 hbo', 'S3_D1 hbo', 'S1_D1 hbr', 'S2_D1 hbr', 'S3_D1 hbr']
ch_types = np.repeat(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
raw.pick(picks=[0, 3, 1, 4, 2, 5])
_check_channels_ordered(raw.info, ['hbo', 'hbr'])
with pytest.raises(ValueError, match='chromophore in info'):
    _check_channels_ordered(raw.info, ['hbb', 'hbr'])
ch_names = ['S1_D1 hbb', 'S1_D1 hbr', 'S2_D1 hbb', 'S2_D1 hbr', 'S3_D1 hbb', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
with pytest.raises(ValueError, match='naming conventions'):
    _check_channels_ordered(raw.info, ['hbo', 'hbr'])
ch_names = ['S1_DX hbo', 'S1_DX hbr', 'S2_D1 hbo', 'S2_D1 hbr', 'S3_D1 hbo', 'S3_D1 hbr']
ch_types = np.tile(['hbo', 'hbr'], 3)
info = create_info(ch_names=ch_names, ch_types=ch_types, sfreq=1.0)
raw = RawArray(data, info, verbose=True)
with pytest.raises(ValueError, match='can not be parsed'):
    _check_channels_ordered(raw.info, ['hbo', 'hbr'])
```

## Next Steps


---

*Source: test_nirs.py:436 | Complexity: Advanced | Last updated: 2026-05-18*