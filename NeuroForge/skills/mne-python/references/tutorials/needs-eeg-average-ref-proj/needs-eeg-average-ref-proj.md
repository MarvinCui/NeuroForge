# How To: Needs Eeg Average Ref Proj

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test checking whether a recording needs an EEG average reference.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.proj`
- `mne.cov`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.proj`
- `mne.rank`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test checking whether a recording needs an EEG average reference.'

```python
'Test checking whether a recording needs an EEG average reference.'
```

**Verification:**
```python
assert _needs_eeg_average_ref_proj(raw.info)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert not _needs_eeg_average_ref_proj(raw.info)
```

### Step 3: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

**Verification:**
```python
assert not _needs_eeg_average_ref_proj(raw.info)
```

### Step 4: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

**Verification:**
```python
assert not _needs_eeg_average_ref_proj(raw.info)
```

### Step 5: Assign eeg = value

```python
eeg = [raw.ch_names[c] for c in pick_types(raw.info, meg=False, eeg=True)]
```

### Step 6: Call raw.drop_channels()

```python
raw.drop_channels(eeg)
```

**Verification:**
```python
assert not _needs_eeg_average_ref_proj(raw.info)
```

### Step 7: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert not _needs_eeg_average_ref_proj(raw.info)
```

### Step 8: Assign unknown = True

```python
raw.info['custom_ref_applied'] = True
```


## Complete Example

```python
# Workflow
'Test checking whether a recording needs an EEG average reference.'
raw = read_raw_fif(raw_fname)
assert _needs_eeg_average_ref_proj(raw.info)
raw.set_eeg_reference(projection=True)
assert not _needs_eeg_average_ref_proj(raw.info)
raw = read_raw_fif(raw_fname, preload=True)
eeg = [raw.ch_names[c] for c in pick_types(raw.info, meg=False, eeg=True)]
raw.drop_channels(eeg)
assert not _needs_eeg_average_ref_proj(raw.info)
raw = read_raw_fif(raw_fname)
with raw.info._unlock():
    raw.info['custom_ref_applied'] = True
assert not _needs_eeg_average_ref_proj(raw.info)
```

## Next Steps


---

*Source: test_proj.py:485 | Complexity: Advanced | Last updated: 2026-05-18*