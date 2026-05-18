# How To: Edf Padding

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test exporting an EDF file with not-equal-length data blocks.

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
# Fixtures: tmp_path, pad_width
```

## Step-by-Step Guide

### Step 1: 'Test exporting an EDF file with not-equal-length data blocks.'

```python
'Test exporting an EDF file with not-equal-length data blocks.'
```

**Verification:**
```python
assert raw.n_times == raw_read.n_times - pad_width
```

### Step 2: Assign ch_types = value

```python
ch_types = ['eeg'] * 4
```

**Verification:**
```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :-pad_width], decimal=10)
```

### Step 3: Assign ch_names = np.arange.astype.tolist(...)

```python
ch_names = np.arange(len(ch_types)).astype(str).tolist()
```

**Verification:**
```python
assert_array_almost_equal(pad_data, np.tile(edge_data, (pad_width, 1)).T, decimal=10)
```

### Step 4: Assign fs = 1000

```python
fs = 1000
```

**Verification:**
```python
assert 'BAD_ACQ_SKIP' in raw_read.annotations.description
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(len(ch_types), sfreq=fs, ch_types=ch_types)
```

**Verification:**
```python
assert_array_almost_equal(raw_read.annotations.onset[0], raw.times[-1] + 1 / fs)
```

### Step 6: Assign data = value

```python
data = np.tile(np.sin(2 * np.pi * 10 * np.arange(0, 2, 1 / fs)) * 1e-05, (len(ch_names), 1))[:, 0:-pad_width]
```

**Verification:**
```python
assert_array_almost_equal(raw_read.annotations.duration[0], pad_width / fs)
```

### Step 7: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 8: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.edf'
```

### Step 9: Assign raw_read = read_raw_edf(...)

```python
raw_read = read_raw_edf(temp_fname, preload=True)
```

**Verification:**
```python
assert raw.n_times == raw_read.n_times - pad_width
```

### Step 10: Assign edge_data = value

```python
edge_data = raw_read.get_data()[:, -pad_width - 1]
```

### Step 11: Assign pad_data = value

```python
pad_data = raw_read.get_data()[:, -pad_width:]
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :-pad_width], decimal=10)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pad_data, np.tile(edge_data, (pad_width, 1)).T, decimal=10)
```

**Verification:**
```python
assert 'BAD_ACQ_SKIP' in raw_read.annotations.description
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw_read.annotations.onset[0], raw.times[-1] + 1 / fs)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw_read.annotations.duration[0], pad_width / fs)
```

### Step 16: Call raw.export()

```python
raw.export(temp_fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, pad_width

# Workflow
'Test exporting an EDF file with not-equal-length data blocks.'
ch_types = ['eeg'] * 4
ch_names = np.arange(len(ch_types)).astype(str).tolist()
fs = 1000
info = create_info(len(ch_types), sfreq=fs, ch_types=ch_types)
data = np.tile(np.sin(2 * np.pi * 10 * np.arange(0, 2, 1 / fs)) * 1e-05, (len(ch_names), 1))[:, 0:-pad_width]
raw = RawArray(data, info)
temp_fname = tmp_path / 'test.edf'
with pytest.warns(RuntimeWarning, match=f'EDF format requires equal-length data blocks.*{pad_width / 1000:.3g} seconds of edge values were appended.*'):
    raw.export(temp_fname)
raw_read = read_raw_edf(temp_fname, preload=True)
assert raw.n_times == raw_read.n_times - pad_width
edge_data = raw_read.get_data()[:, -pad_width - 1]
pad_data = raw_read.get_data()[:, -pad_width:]
assert_array_almost_equal(raw.get_data(), raw_read.get_data()[:, :-pad_width], decimal=10)
assert_array_almost_equal(pad_data, np.tile(edge_data, (pad_width, 1)).T, decimal=10)
assert 'BAD_ACQ_SKIP' in raw_read.annotations.description
assert_array_almost_equal(raw_read.annotations.onset[0], raw.times[-1] + 1 / fs)
assert_array_almost_equal(raw_read.annotations.duration[0], pad_width / fs)
```

## Next Steps


---

*Source: test_export.py:267 | Complexity: Advanced | Last updated: 2026-05-18*