# How To: Nirs Channel Grouping

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test channel grouping related errors.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: fname, readerfn
```

## Step-by-Step Guide

### Step 1: 'Test channel grouping related errors.'

```python
'Test channel grouping related errors.'
```

**Verification:**
```python
assert len(picks) == len(raw.ch_names)
```

### Step 2: Assign raw = readerfn(...)

```python
raw = readerfn(fname)
```

### Step 3: Assign freqs = np.unique.tolist(...)

```python
freqs = np.unique(_channel_frequencies(raw.info)).tolist()
```

### Step 4: Assign nfreqs = len(...)

```python
nfreqs = len(freqs)
```

### Step 5: Assign picks = _check_channels_ordered(...)

```python
picks = _check_channels_ordered(raw.info, freqs)
```

**Verification:**
```python
assert len(picks) == len(raw.ch_names)
```

### Step 6: Assign raw_dropped = raw.copy.drop_channels(...)

```python
raw_dropped = raw.copy().drop_channels(raw.ch_names[4])
```

### Step 7: Assign raw_incomplete = raw.copy.pick(...)

```python
raw_incomplete = raw.copy().pick(list(range(nfreqs + 1)))
```

### Step 8: Assign raw_extrafreq = raw.copy(...)

```python
raw_extrafreq = raw.copy()
```

### Step 9: Assign new_ch10_name = value

```python
new_ch10_name = f"{raw_extrafreq.ch_names[10].split(' ')[0]} 100"
```

### Step 10: Call raw_extrafreq.rename_channels()

```python
raw_extrafreq.rename_channels({raw_extrafreq.ch_names[10]: new_ch10_name})
```

### Step 11: Call print()

```python
print(raw_extrafreq.ch_names)
```

### Step 12: Assign raw_locnone = raw.copy(...)

```python
raw_locnone = raw.copy()
```

### Step 13: Assign unknown = None

```python
raw_locnone.info['chs'][10]['loc'][9] = None
```

### Step 14: Call _check_channels_ordered()

```python
_check_channels_ordered(raw_dropped.info, freqs)
```

### Step 15: Call _check_channels_ordered()

```python
_check_channels_ordered(raw_incomplete.info, freqs)
```

### Step 16: Call _check_channels_ordered()

```python
_check_channels_ordered(raw_extrafreq.info, [100] + freqs)
```

### Step 17: Call _check_channels_ordered()

```python
_check_channels_ordered(raw_extrafreq.info, freqs)
```

### Step 18: Call _check_channels_ordered()

```python
_check_channels_ordered(raw_locnone.info, freqs)
```


## Complete Example

```python
# Setup
# Fixtures: fname, readerfn

# Workflow
'Test channel grouping related errors.'
raw = readerfn(fname)
freqs = np.unique(_channel_frequencies(raw.info)).tolist()
nfreqs = len(freqs)
picks = _check_channels_ordered(raw.info, freqs)
assert len(picks) == len(raw.ch_names)
raw_dropped = raw.copy().drop_channels(raw.ch_names[4])
with pytest.raises(ValueError, match='NIRS channels not ordered correctly.'):
    _check_channels_ordered(raw_dropped.info, freqs)
raw_incomplete = raw.copy().pick(list(range(nfreqs + 1)))
with pytest.raises(ValueError, match='NIRS channels not ordered correctly.'):
    _check_channels_ordered(raw_incomplete.info, freqs)
raw_extrafreq = raw.copy()
new_ch10_name = f"{raw_extrafreq.ch_names[10].split(' ')[0]} 100"
raw_extrafreq.rename_channels({raw_extrafreq.ch_names[10]: new_ch10_name})
print(raw_extrafreq.ch_names)
with pytest.raises(ValueError, match='NIRS channels not ordered correctly.'):
    _check_channels_ordered(raw_extrafreq.info, [100] + freqs)
with pytest.raises(ValueError, match='NIRS channels not ordered correctly.'):
    _check_channels_ordered(raw_extrafreq.info, freqs)
raw_locnone = raw.copy()
raw_locnone.info['chs'][10]['loc'][9] = None
with pytest.raises(ValueError, match='NIRS channels is missing wavelength information'):
    _check_channels_ordered(raw_locnone.info, freqs)
```

## Next Steps


---

*Source: test_nirs.py:627 | Complexity: Advanced | Last updated: 2026-05-18*