# How To: Make Eeg Average Ref Proj

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test EEG average reference projection.

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

### Step 1: 'Test EEG average reference projection.'

```python
'Test EEG average reference projection.'
```

**Verification:**
```python
assert not np.all(raw._data[eeg].mean(axis=0) < 1e-19)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname, preload=True)
```

**Verification:**
```python
assert_array_almost_equal(reref._data[eeg].mean(axis=0), 0, decimal=18)
```

### Step 3: Assign eeg = pick_types(...)

```python
eeg = pick_types(raw.info, meg=False, eeg=True)
```

**Verification:**
```python
assert _has_eeg_average_ref_proj(raw.info)
```

### Step 4: Assign car = make_eeg_average_ref_proj(...)

```python
car = make_eeg_average_ref_proj(raw.info)
```

**Verification:**
```python
assert not _has_eeg_average_ref_proj(raw.info)
```

### Step 5: Assign reref = raw.copy(...)

```python
reref = raw.copy()
```

**Verification:**
```python
assert not _has_eeg_average_ref_proj(raw.info)
```

### Step 6: Call reref.add_proj()

```python
reref.add_proj(car)
```

### Step 7: Call reref.apply_proj()

```python
reref.apply_proj()
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(reref._data[eeg].mean(axis=0), 0, decimal=18)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(RuntimeError, make_eeg_average_ref_proj, raw.info)
```

### Step 10: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

**Verification:**
```python
assert _has_eeg_average_ref_proj(raw.info)
```

### Step 11: Call raw.del_proj()

```python
raw.del_proj(idx=-1)
```

**Verification:**
```python
assert not _has_eeg_average_ref_proj(raw.info)
```

### Step 12: Call raw.apply_proj()

```python
raw.apply_proj()
```

**Verification:**
```python
assert not _has_eeg_average_ref_proj(raw.info)
```

### Step 13: Assign unknown = True

```python
raw.info['custom_ref_applied'] = True
```


## Complete Example

```python
# Workflow
'Test EEG average reference projection.'
raw = read_raw_fif(raw_fname, preload=True)
eeg = pick_types(raw.info, meg=False, eeg=True)
assert not np.all(raw._data[eeg].mean(axis=0) < 1e-19)
car = make_eeg_average_ref_proj(raw.info)
reref = raw.copy()
reref.add_proj(car)
reref.apply_proj()
assert_array_almost_equal(reref._data[eeg].mean(axis=0), 0, decimal=18)
with raw.info._unlock():
    raw.info['custom_ref_applied'] = True
pytest.raises(RuntimeError, make_eeg_average_ref_proj, raw.info)
raw.set_eeg_reference(projection=True)
assert _has_eeg_average_ref_proj(raw.info)
raw.del_proj(idx=-1)
assert not _has_eeg_average_ref_proj(raw.info)
raw.apply_proj()
assert not _has_eeg_average_ref_proj(raw.info)
```

## Next Steps


---

*Source: test_proj.py:362 | Complexity: Advanced | Last updated: 2026-05-18*