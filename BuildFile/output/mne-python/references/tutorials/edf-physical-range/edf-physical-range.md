# How To: Edf Physical Range

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test exporting an EDF file with different physical range settings.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test exporting an EDF file with different physical range settings.'

```python
'Test exporting an EDF file with different physical range settings.'
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 2: Assign ch_types = value

```python
ch_types = ['eeg'] * 4
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 3: Assign ch_names = np.arange.astype.tolist(...)

```python
ch_names = np.arange(len(ch_types)).astype(str).tolist()
```

### Step 4: Assign fs = 1000

```python
fs = 1000
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(len(ch_types), sfreq=fs, ch_types=ch_types)
```

### Step 6: Assign data = np.tile(...)

```python
data = np.tile(np.sin(2 * np.pi * 10 * np.arange(0, 2, 1 / fs)) * 1e-05, (len(ch_names), 1))
```

### Step 7: Assign data = value

```python
data = (data.T + [0.1, 0, 0, -0.1]).T
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 9: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test_auto.edf'
```

### Step 10: Call raw.export()

```python
raw.export(temp_fname)
```

### Step 11: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, preload=True)
```

### Step 12: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test_per_channel.edf'
```

### Step 13: Call raw.export()

```python
raw.export(temp_fname, physical_range='channelwise')
```

### Step 14: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, preload=True)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test exporting an EDF file with different physical range settings.'
ch_types = ['eeg'] * 4
ch_names = np.arange(len(ch_types)).astype(str).tolist()
fs = 1000
info = create_info(len(ch_types), sfreq=fs, ch_types=ch_types)
data = np.tile(np.sin(2 * np.pi * 10 * np.arange(0, 2, 1 / fs)) * 1e-05, (len(ch_names), 1))
data = (data.T + [0.1, 0, 0, -0.1]).T
raw = RawArray(data, info)
temp_fname = tmp_path / 'test_auto.edf'
raw.export(temp_fname)
raw_read = read_raw_edf(temp_fname, preload=True)
with pytest.raises(AssertionError, match='Arrays are not almost equal'):
    assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
temp_fname = tmp_path / 'test_per_channel.edf'
raw.export(temp_fname, physical_range='channelwise')
raw_read = read_raw_edf(temp_fname, preload=True)
assert_array_almost_equal(raw.get_data(), raw_read.get_data(), decimal=10)
```

## Next Steps


---

*Source: test_export.py:239 | Complexity: Advanced | Last updated: 2026-05-18*