# How To: Add Reorder

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that a reference channel can be added and then data reordered.

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
# Fixtures: n_ref
```

## Step-by-Step Guide

### Step 1: 'Test that a reference channel can be added and then data reordered.'

```python
'Test that a reference channel can be added and then data reordered.'
```

**Verification:**
```python
assert len(raw.ch_names) == 60
```

### Step 2: Assign raw = read_raw_fif.crop.del_proj.pick(...)

```python
raw = read_raw_fif(raw_fname).crop(0, 0.1).del_proj().pick('eeg')
```

**Verification:**
```python
assert n_ref == 2
```

### Step 3: Assign chs = value

```python
chs = [f'EEG {60 + ii:03}' for ii in range(1, n_ref)] + ['EEG 000']
```

**Verification:**
```python
assert_array_equal(data[-1], 0.0)
```

### Step 4: Call raw.load_data()

```python
raw.load_data()
```

**Verification:**
```python
assert raw.ch_names[-n_ref:] == chs
```

### Step 5: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert raw.ch_names == [f'EEG {ii:03}' for ii in range(60 + n_ref)]
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(data[-1], 0.0)
```

**Verification:**
```python
assert_allclose(data, data_new)
```

### Step 7: Call raw.reorder_channels()

```python
raw.reorder_channels(raw.ch_names[-1:] + raw.ch_names[:-1])
```

**Verification:**
```python
assert raw.ch_names == [f'EEG {ii:03}' for ii in range(60 + n_ref)]
```

### Step 8: Assign data_new = raw.get_data(...)

```python
data_new = raw.get_data()
```

### Step 9: Assign data_new = np.concatenate(...)

```python
data_new = np.concatenate([data_new[1:], data_new[:1]])
```

### Step 10: Call assert_allclose()

```python
assert_allclose(data, data_new)
```

### Step 11: Assign ctx = nullcontext(...)

```python
ctx = nullcontext()
```

**Verification:**
```python
assert n_ref == 2
```

### Step 12: Assign ctx = pytest.warns(...)

```python
ctx = pytest.warns(RuntimeWarning, match='this channel is unknown or ambiguous')
```

### Step 13: Call add_reference_channels()

```python
add_reference_channels(raw, chs, copy=False)
```

### Step 14: Call add_reference_channels()

```python
add_reference_channels(raw, chs, copy=False)
```


## Complete Example

```python
# Setup
# Fixtures: n_ref

# Workflow
'Test that a reference channel can be added and then data reordered.'
raw = read_raw_fif(raw_fname).crop(0, 0.1).del_proj().pick('eeg')
assert len(raw.ch_names) == 60
chs = [f'EEG {60 + ii:03}' for ii in range(1, n_ref)] + ['EEG 000']
with pytest.raises(RuntimeError, match='preload'):
    with _record_warnings():
        add_reference_channels(raw, chs, copy=False)
raw.load_data()
if n_ref == 1:
    ctx = nullcontext()
else:
    assert n_ref == 2
    ctx = pytest.warns(RuntimeWarning, match='this channel is unknown or ambiguous')
with ctx:
    add_reference_channels(raw, chs, copy=False)
data = raw.get_data()
assert_array_equal(data[-1], 0.0)
assert raw.ch_names[-n_ref:] == chs
raw.reorder_channels(raw.ch_names[-1:] + raw.ch_names[:-1])
assert raw.ch_names == [f'EEG {ii:03}' for ii in range(60 + n_ref)]
data_new = raw.get_data()
data_new = np.concatenate([data_new[1:], data_new[:1]])
assert_allclose(data, data_new)
```

## Next Steps


---

*Source: test_reference.py:893 | Complexity: Advanced | Last updated: 2026-05-18*