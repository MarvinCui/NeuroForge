# How To: Export Raw Pybv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test saving a Raw instance to BrainVision format via pybv.

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
# Fixtures: tmp_path, meas_date, orig_time, ext
```

## Step-by-Step Guide

### Step 1: 'Test saving a Raw instance to BrainVision format via pybv.'

```python
'Test saving a Raw instance to BrainVision format via pybv.'
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('pybv')
```

**Verification:**
```python
assert_allclose(raw.times, raw_read.times)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw, preload=True)
```

**Verification:**
```python
assert_allclose(raw.get_data(), raw_read.get_data())
```

### Step 4: Call raw.apply_proj()

```python
raw.apply_proj()
```

### Step 5: Call raw.set_meas_date()

```python
raw.set_meas_date(meas_date)
```

### Step 6: Assign annots = Annotations(...)

```python
annots = Annotations(onset=[3, 6, 9, 12, 14], duration=[1, 1, 0.5, 0.25, 9], description=['Stimulus/S  1', 'Stimulus/S2.50', 'Response/R101', 'Look at this', 'Comment/And at this'], ch_names=[(), (), (), ('EEG 001',), ('EEG 001', 'EEG 002')], orig_time=orig_time)
```

### Step 7: Call raw.set_annotations()

```python
raw.set_annotations(annots)
```

### Step 8: Assign temp_fname = value

```python
temp_fname = tmp_path / ('test' + ext)
```

### Step 9: Assign raw_read = read_raw_brainvision(...)

```python
raw_read = read_raw_brainvision(str(temp_fname).replace('.eeg', '.vhdr'))
```

**Verification:**
```python
assert raw.ch_names == raw_read.ch_names
```

### Step 10: Call assert_allclose()

```python
assert_allclose(raw.times, raw_read.times)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw.get_data(), raw_read.get_data())
```

### Step 12: Call raw.export()

```python
raw.export(temp_fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, meas_date, orig_time, ext

# Workflow
'Test saving a Raw instance to BrainVision format via pybv.'
pytest.importorskip('pybv')
raw = read_raw_fif(fname_raw, preload=True)
raw.apply_proj()
raw.set_meas_date(meas_date)
annots = Annotations(onset=[3, 6, 9, 12, 14], duration=[1, 1, 0.5, 0.25, 9], description=['Stimulus/S  1', 'Stimulus/S2.50', 'Response/R101', 'Look at this', 'Comment/And at this'], ch_names=[(), (), (), ('EEG 001',), ('EEG 001', 'EEG 002')], orig_time=orig_time)
raw.set_annotations(annots)
temp_fname = tmp_path / ('test' + ext)
with _record_warnings(), pytest.warns(RuntimeWarning, match="'short' format. Converting"):
    raw.export(temp_fname)
raw_read = read_raw_brainvision(str(temp_fname).replace('.eeg', '.vhdr'))
assert raw.ch_names == raw_read.ch_names
assert_allclose(raw.times, raw_read.times)
assert_allclose(raw.get_data(), raw_read.get_data())
```

## Next Steps


---

*Source: test_export.py:58 | Complexity: Advanced | Last updated: 2026-05-18*