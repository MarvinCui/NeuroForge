# How To: Export Raw Eeglab

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test saving a Raw instance to EEGLAB's set format.

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

### Step 1: "Test saving a Raw instance to EEGLAB's set format."

```python
"Test saving a Raw instance to EEGLAB's set format."
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('eeglabio')
```

**Verification:**
```python
assert_allclose(cart_coords, cart_coords_read)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw, preload=True)
```

**Verification:**
```python
assert_allclose(raw.times, raw_read.times)
```

### Step 4: Call raw.apply_proj()

```python
raw.apply_proj()
```

**Verification:**
```python
assert_allclose(raw.get_data(), raw_read.get_data())
```

### Step 5: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.set'
```

### Step 6: Call raw.export()

```python
raw.export(temp_fname)
```

### Step 7: Call raw.drop_channels()

```python
raw.drop_channels([ch for ch in ['epoc'] if ch in raw.ch_names])
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 8: Assign cart_coords = np.array(...)

```python
cart_coords = np.array([d['loc'][:3] for d in raw.info['chs']])
```

### Step 9: Assign cart_coords_read = np.array(...)

```python
cart_coords_read = np.array([d['loc'][:3] for d in raw_read.info['chs']])
```

### Step 10: Call assert_allclose()

```python
assert_allclose(cart_coords, cart_coords_read)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw.times, raw_read.times)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw.get_data(), raw_read.get_data())
```

### Step 13: Call raw.export()

```python
raw.export(temp_fname, overwrite=True)
```

### Step 14: Call raw.export()

```python
raw.export(Path(temp_fname), overwrite=True)
```

### Step 15: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw, preload=True)
```

### Step 16: Assign raw_read = read_raw_eeglab(...)

```python
raw_read = read_raw_eeglab(temp_fname, preload=True, montage_units='m')
```

### Step 17: Call raw.export()

```python
raw.export(temp_fname, overwrite=False)
```

### Step 18: Call raw.export()

```python
raw.export(temp_fname, overwrite=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
"Test saving a Raw instance to EEGLAB's set format."
pytest.importorskip('eeglabio')
raw = read_raw_fif(fname_raw, preload=True)
raw.apply_proj()
temp_fname = tmp_path / 'test.set'
raw.export(temp_fname)
raw.drop_channels([ch for ch in ['epoc'] if ch in raw.ch_names])
with pytest.warns(RuntimeWarning, match='is above the 99th percentile'):
    raw_read = read_raw_eeglab(temp_fname, preload=True, montage_units='m')
assert raw.ch_names == raw_read.ch_names
cart_coords = np.array([d['loc'][:3] for d in raw.info['chs']])
cart_coords_read = np.array([d['loc'][:3] for d in raw_read.info['chs']])
assert_allclose(cart_coords, cart_coords_read)
assert_allclose(raw.times, raw_read.times)
assert_allclose(raw.get_data(), raw_read.get_data())
with pytest.raises(FileExistsError, match='Destination file exists'):
    raw.export(temp_fname, overwrite=False)
raw.export(temp_fname, overwrite=True)
raw.export(Path(temp_fname), overwrite=True)
raw = read_raw_fif(fname_raw, preload=True)
with pytest.warns(RuntimeWarning, match='Raw instance has unapplied projectors.'):
    raw.export(temp_fname, overwrite=True)
```

## Next Steps


---

*Source: test_export.py:94 | Complexity: Advanced | Last updated: 2026-05-18*