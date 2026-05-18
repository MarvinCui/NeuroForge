# How To: Export Raw Edf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test saving a Raw instance to EDF format.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.export`
- `mne.fixes`
- `mne.io`
- `mne.tests.test_epochs`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, input_path, warning_msg
```

## Step-by-Step Guide

### Step 1: 'Test saving a Raw instance to EDF format.'

```python
'Test saving a Raw instance to EDF format.'
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(input_path)
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :orig_raw_len], decimal=8)
```

### Step 3: Call raw.pick.load_data()

```python
raw.pick(picks=['eeg', 'ecog', 'seeg']).load_data()
```

**Verification:**
```python
assert_allclose(raw.times, raw_read.times[:orig_raw_len], rtol=0, atol=1e-05)
```

### Step 4: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.edf'
```

### Step 5: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, preload=True)
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 6: Assign orig_raw_len = len(...)

```python
orig_raw_len = len(raw)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :orig_raw_len], decimal=8)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(raw.times, raw_read.times[:orig_raw_len], rtol=0, atol=1e-05)
```

### Step 9: Call raw.export()

```python
raw.export(temp_fname)
```

### Step 10: Call raw.drop_channels()

```python
raw.drop_channels(['epoc'])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, input_path, warning_msg

# Workflow
'Test saving a Raw instance to EDF format.'
raw = read_raw_fif(input_path)
raw.pick(picks=['eeg', 'ecog', 'seeg']).load_data()
temp_fname = tmp_path / 'test.edf'
with pytest.warns(RuntimeWarning, match=warning_msg):
    raw.export(temp_fname)
if 'epoc' in raw.ch_names:
    raw.drop_channels(['epoc'])
raw_read = read_raw_edf(temp_fname, preload=True)
assert raw.ch_names == raw_read.ch_names
orig_raw_len = len(raw)
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :orig_raw_len], decimal=8)
assert_allclose(raw.times, raw_read.times[:orig_raw_len], rtol=0, atol=1e-05)
```

## Next Steps


---

*Source: test_export.py:481 | Complexity: Advanced | Last updated: 2026-05-18*