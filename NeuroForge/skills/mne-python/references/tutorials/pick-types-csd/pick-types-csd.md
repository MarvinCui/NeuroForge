# How To: Pick Types Csd

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test pick_types(csd=True).

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

### Step 1: 'Test pick_types(csd=True).'

```python
'Test pick_types(csd=True).'
```

**Verification:**
```python
assert_array_equal(pick_types(info1, csd=True), [7])
```

### Step 2: Assign names = value

```python
names = ['F1', 'F2', 'C1', 'C2', 'A1', 'A2', 'misc1', 'CSD1']
```

**Verification:**
```python
assert raw_csd.copy().pick('csd').ch_names == ['F1', 'F2', 'C1', 'C2', 'CSD1']
```

### Step 3: Assign info1 = create_info(...)

```python
info1 = create_info(names, 256, ['eeg', 'eeg', 'eeg', 'eeg', 'mag', 'mag', 'misc', 'csd'])
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(np.zeros((8, 512)), info1)
```

### Step 5: Call raw.set_montage()

```python
raw.set_montage(make_standard_montage('standard_1020'), verbose='error')
```

### Step 6: Assign raw_csd = compute_current_source_density(...)

```python
raw_csd = compute_current_source_density(raw, verbose='error')
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(pick_types(info1, csd=True), [7])
```

**Verification:**
```python
assert raw_csd.copy().pick('csd').ch_names == ['F1', 'F2', 'C1', 'C2', 'CSD1']
```


## Complete Example

```python
# Workflow
'Test pick_types(csd=True).'
names = ['F1', 'F2', 'C1', 'C2', 'A1', 'A2', 'misc1', 'CSD1']
info1 = create_info(names, 256, ['eeg', 'eeg', 'eeg', 'eeg', 'mag', 'mag', 'misc', 'csd'])
raw = RawArray(np.zeros((8, 512)), info1)
raw.set_montage(make_standard_montage('standard_1020'), verbose='error')
raw_csd = compute_current_source_density(raw, verbose='error')
assert_array_equal(pick_types(info1, csd=True), [7])
assert raw_csd.copy().pick('csd').ch_names == ['F1', 'F2', 'C1', 'C2', 'CSD1']
```

## Next Steps


---

*Source: test_pick.py:725 | Complexity: Intermediate | Last updated: 2026-05-18*