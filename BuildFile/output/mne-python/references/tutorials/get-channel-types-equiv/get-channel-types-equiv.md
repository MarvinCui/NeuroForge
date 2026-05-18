# How To: Get Channel Types Equiv

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test equivalence of get_channel_types.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: meg, eeg, ordered
```

## Step-by-Step Guide

### Step 1: 'Test equivalence of get_channel_types.'

```python
'Test equivalence of get_channel_types.'
```

**Verification:**
```python
assert_array_equal(types, types_iter)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fif_fname)
```

### Step 3: Call pick_types()

```python
pick_types(raw.info, meg=meg, eeg=eeg)
```

### Step 4: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=meg, eeg=eeg)
```

### Step 5: Assign types = np.array(...)

```python
types = np.array(raw.get_channel_types(picks=picks))
```

### Step 6: Assign types_iter = np.array(...)

```python
types_iter = np.array([channel_type(raw.info, idx) for idx in picks])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(types, types_iter)
```

### Step 8: Assign picks = np.random.RandomState.permutation(...)

```python
picks = np.random.RandomState(0).permutation(picks)
```

### Step 9: Call raw.get_channel_types()

```python
raw.get_channel_types(picks=picks)
```


## Complete Example

```python
# Setup
# Fixtures: meg, eeg, ordered

# Workflow
'Test equivalence of get_channel_types.'
raw = read_raw_fif(fif_fname)
pick_types(raw.info, meg=meg, eeg=eeg)
picks = pick_types(raw.info, meg=meg, eeg=eeg)
if not ordered:
    picks = np.random.RandomState(0).permutation(picks)
if not meg and (not eeg):
    with pytest.raises(ValueError, match='No appropriate channels'):
        raw.get_channel_types(picks=picks)
    return
types = np.array(raw.get_channel_types(picks=picks))
types_iter = np.array([channel_type(raw.info, idx) for idx in picks])
assert_array_equal(types, types_iter)
```

## Next Steps


---

*Source: test_pick.py:751 | Complexity: Advanced | Last updated: 2026-05-18*