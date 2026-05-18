# How To: Export Raw Eeglab Annotations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test annotations in the exported EEGLAB file.

All annotations should be preserved and onset corrected.

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
# Fixtures: tmp_path, tmin
```

## Step-by-Step Guide

### Step 1: 'Test annotations in the exported EEGLAB file.\n\n    All annotations should be preserved and onset corrected.\n    '

```python
'Test annotations in the exported EEGLAB file.\n\n    All annotations should be preserved and onset corrected.\n    '
```

**Verification:**
```python
assert raw_read.first_time == 0
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('eeglabio')
```

**Verification:**
```python
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_raw, preload=True)
```

**Verification:**
```python
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
```

### Step 4: Call raw.apply_proj()

```python
raw.apply_proj()
```

**Verification:**
```python
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
```

### Step 5: Assign annotations = Annotations(...)

```python
annotations = Annotations(onset=[0.01, 0.05, 0.9, 1.05], duration=[0, 1, 0, 0], description=['test1', 'test2', 'test3', 'test4'], ch_names=[['MEG 0113'], ['MEG 0113', 'MEG 0132'], [], ['MEG 0143']])
```

### Step 6: Call raw.set_annotations()

```python
raw.set_annotations(annotations)
```

### Step 7: Call raw.crop()

```python
raw.crop(tmin)
```

### Step 8: Assign temp_fname = value

```python
temp_fname = tmp_path / 'test.set'
```

### Step 9: Call raw.export()

```python
raw.export(temp_fname)
```

**Verification:**
```python
assert raw_read.first_time == 0
```

### Step 10: Assign valid_annot = value

```python
valid_annot = raw.annotations.onset >= tmin
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
```

### Step 14: Assign raw_read = read_raw_eeglab(...)

```python
raw_read = read_raw_eeglab(temp_fname, preload=True, montage_units='m')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, tmin

# Workflow
'Test annotations in the exported EEGLAB file.\n\n    All annotations should be preserved and onset corrected.\n    '
pytest.importorskip('eeglabio')
raw = read_raw_fif(fname_raw, preload=True)
raw.apply_proj()
annotations = Annotations(onset=[0.01, 0.05, 0.9, 1.05], duration=[0, 1, 0, 0], description=['test1', 'test2', 'test3', 'test4'], ch_names=[['MEG 0113'], ['MEG 0113', 'MEG 0132'], [], ['MEG 0143']])
raw.set_annotations(annotations)
raw.crop(tmin)
temp_fname = tmp_path / 'test.set'
raw.export(temp_fname)
with pytest.warns(RuntimeWarning, match='is above the 99th percentile'):
    raw_read = read_raw_eeglab(temp_fname, preload=True, montage_units='m')
assert raw_read.first_time == 0
valid_annot = raw.annotations.onset >= tmin
assert_array_almost_equal(raw.annotations.onset[valid_annot] - raw.first_time, raw_read.annotations.onset)
assert_array_equal(raw.annotations.duration[valid_annot], raw_read.annotations.duration)
assert_array_equal(raw.annotations.description[valid_annot], raw_read.annotations.description)
```

## Next Steps


---

*Source: test_export.py:128 | Complexity: Advanced | Last updated: 2026-05-18*