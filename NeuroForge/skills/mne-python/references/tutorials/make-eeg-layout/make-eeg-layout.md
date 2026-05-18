# How To: Make Eeg Layout

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test creation of EEG layout.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne.channels`
- `mne.channels.layout`
- `mne.defaults`
- `mne.io`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test creation of EEG layout.'

```python
'Test creation of EEG layout.'
```

**Verification:**
```python
assert_array_equal(len(layout.names), len([ch for ch in info['ch_names'] if ch.startswith('EE')]))
```

### Step 2: Assign lout_orig = read_layout(...)

```python
lout_orig = read_layout(fname=lout_path / 'test_raw.lout')
```

**Verification:**
```python
assert_array_equal(lout_new.kind, 'foo')
```

### Step 3: Assign info = read_info(...)

```python
info = read_info(fif_fname)
```

**Verification:**
```python
assert_allclose(layout.pos, lout_new.pos, atol=0.1)
```

### Step 4: Call unknown.append()

```python
info['bads'].append(info['ch_names'][360])
```

**Verification:**
```python
assert_array_equal(lout_orig.names, lout_new.names)
```

### Step 5: Assign layout = make_eeg_layout(...)

```python
layout = make_eeg_layout(info, exclude=[])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(len(layout.names), len([ch for ch in info['ch_names'] if ch.startswith('EE')]))
```

### Step 7: Call layout.save()

```python
layout.save(str(tmp_path / 'foo.lout'))
```

### Step 8: Assign lout_new = read_layout(...)

```python
lout_new = read_layout(fname=tmp_path / 'foo.lout', scale=False)
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(lout_new.kind, 'foo')
```

### Step 10: Call assert_allclose()

```python
assert_allclose(layout.pos, lout_new.pos, atol=0.1)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(lout_orig.names, lout_new.names)
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, radius=-0.1)
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, radius=0.6)
```

### Step 14: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, width=-0.1)
```

### Step 15: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, width=1.1)
```

### Step 16: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, height=-0.1)
```

### Step 17: Call pytest.raises()

```python
pytest.raises(ValueError, make_eeg_layout, info, height=1.1)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test creation of EEG layout.'
lout_orig = read_layout(fname=lout_path / 'test_raw.lout')
info = read_info(fif_fname)
info['bads'].append(info['ch_names'][360])
layout = make_eeg_layout(info, exclude=[])
assert_array_equal(len(layout.names), len([ch for ch in info['ch_names'] if ch.startswith('EE')]))
layout.save(str(tmp_path / 'foo.lout'))
lout_new = read_layout(fname=tmp_path / 'foo.lout', scale=False)
assert_array_equal(lout_new.kind, 'foo')
assert_allclose(layout.pos, lout_new.pos, atol=0.1)
assert_array_equal(lout_orig.names, lout_new.names)
pytest.raises(ValueError, make_eeg_layout, info, radius=-0.1)
pytest.raises(ValueError, make_eeg_layout, info, radius=0.6)
pytest.raises(ValueError, make_eeg_layout, info, width=-0.1)
pytest.raises(ValueError, make_eeg_layout, info, width=1.1)
pytest.raises(ValueError, make_eeg_layout, info, height=-0.1)
pytest.raises(ValueError, make_eeg_layout, info, height=1.1)
```

## Next Steps


---

*Source: test_layout.py:189 | Complexity: Advanced | Last updated: 2026-05-18*