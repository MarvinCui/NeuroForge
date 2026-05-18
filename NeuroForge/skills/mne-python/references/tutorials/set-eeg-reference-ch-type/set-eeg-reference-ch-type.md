# How To: Set Eeg Reference Ch Type

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test setting EEG reference for ECoG or DBS.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `contextlib`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne._fiff.reference`
- `mne.datasets`
- `mne.epochs`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: ch_type, msg, projection
```

## Step-by-Step Guide

### Step 1: 'Test setting EEG reference for ECoG or DBS.'

```python
'Test setting EEG reference for ECoG or DBS.'
```

**Verification:**
```python
assert f'Applying a custom {msg}' in log.getvalue()
```

### Step 2: Assign ch_names = value

```python
ch_names = ['ECOG01', 'ECOG02', 'DBS01', 'DBS02', 'MISC']
```

**Verification:**
```python
assert reref.info['custom_ref_applied']
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 4: Assign data = rng.randn(...)

```python
data = rng.randn(5, 1000)
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(data, create_info(ch_names, 1000.0, ['ecog'] * 2 + ['dbs'] * 2 + ['misc']))
```

### Step 6: Call _test_reference()

```python
_test_reference(raw, reref, ref_data, ref_ch)
```

### Step 7: Assign match = value

```python
match = 'no EEG data found' if projection else 'No channels supplied'
```

### Step 8: Assign raw2 = RawArray(...)

```python
raw2 = RawArray(data, create_info(5, 1000.0, ['mag'] * 4 + ['misc']))
```

### Step 9: Assign ref_ch = value

```python
ref_ch = ch_names[:2]
```

### Step 10: Assign ref_ch = value

```python
ref_ch = raw.copy().pick(picks=ch_type).ch_names
```

### Step 11: Assign unknown = set_eeg_reference(...)

```python
reref, ref_data = set_eeg_reference(raw.copy(), ch_type=ch_type, projection=projection, verbose=True)
```

**Verification:**
```python
assert f'Applying a custom {msg}' in log.getvalue()
```

### Step 12: Call set_eeg_reference()

```python
set_eeg_reference(raw, ch_type='eeg', projection=projection)
```

### Step 13: Call set_eeg_reference()

```python
set_eeg_reference(raw2, ch_type='auto', projection=projection)
```


## Complete Example

```python
# Setup
# Fixtures: ch_type, msg, projection

# Workflow
'Test setting EEG reference for ECoG or DBS.'
ch_names = ['ECOG01', 'ECOG02', 'DBS01', 'DBS02', 'MISC']
rng = np.random.RandomState(0)
data = rng.randn(5, 1000)
raw = RawArray(data, create_info(ch_names, 1000.0, ['ecog'] * 2 + ['dbs'] * 2 + ['misc']))
if ch_type == 'auto':
    ref_ch = ch_names[:2]
else:
    ref_ch = raw.copy().pick(picks=ch_type).ch_names
with catch_logging() as log:
    reref, ref_data = set_eeg_reference(raw.copy(), ch_type=ch_type, projection=projection, verbose=True)
if not projection:
    assert f'Applying a custom {msg}' in log.getvalue()
    assert reref.info['custom_ref_applied']
_test_reference(raw, reref, ref_data, ref_ch)
match = 'no EEG data found' if projection else 'No channels supplied'
with pytest.raises(ValueError, match=match):
    set_eeg_reference(raw, ch_type='eeg', projection=projection)
raw2 = RawArray(data, create_info(5, 1000.0, ['mag'] * 4 + ['misc']))
with pytest.raises(ValueError, match='No EEG, ECoG, sEEG or DBS channels found to rereference.'):
    set_eeg_reference(raw2, ch_type='auto', projection=projection)
```

## Next Steps


---

*Source: test_reference.py:271 | Complexity: Advanced | Last updated: 2026-05-18*