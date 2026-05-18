# How To: Nirx 15 2

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading NIRX files.

## Prerequisites

**Required Modules:**
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test reading NIRX files.'

```python
'Test reading NIRX files.'
```

**Verification:**
```python
assert raw._data.shape == (64, 67)
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname_nirx_15_2, preload=True)
```

**Verification:**
```python
assert raw.info['sfreq'] == 3.90625
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description, ['4.0', '6.0', '2.0'])
```

**Verification:**
```python
assert raw.info['meas_date'] == dt.datetime(2019, 10, 2, 9, 8, 47, 511000, tzinfo=dt.timezone.utc)
```

### Step 4: Call print()

```python
print(raw.annotations.onset)
```

**Verification:**
```python
assert raw.info['ch_names'][:4] == ['S1_D1 760', 'S1_D1 850', 'S1_D10 760', 'S1_D10 850']
```

### Step 5: Assign allowed_dist_error = 0.0002

```python
allowed_dist_error = 0.0002
```

**Verification:**
```python
assert raw.info['subject_info'] == dict(sex=1, first_name='TestRecording', birthday=dt.date(1989, 10, 2), his_id='TestRecording')
```

### Step 6: Assign locs = value

```python
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
```

**Verification:**
```python
assert_array_equal(raw.annotations.description, ['4.0', '6.0', '2.0'])
```

### Step 7: Assign unknown = _get_trans(...)

```python
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
```

**Verification:**
```python
assert raw.info['ch_names'][0][3:5] == 'D1'
```

### Step 8: Assign mni_locs = apply_trans(...)

```python
mni_locs = apply_trans(head_mri_t, locs)
```

**Verification:**
```python
assert_allclose(mni_locs[0], [-0.0292, 0.0852, -0.0142], atol=allowed_dist_error)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(mni_locs[0], [-0.0292, 0.0852, -0.0142], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.info['ch_names'][15][3:5] == 'D4'
```

### Step 10: Call assert_allclose()

```python
assert_allclose(mni_locs[15], [-0.0739, -0.0756, -0.0075], atol=allowed_dist_error)
```

**Verification:**
```python
assert_allclose(mni_locs[15], [-0.0739, -0.0756, -0.0075], atol=allowed_dist_error)
```

### Step 11: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, fnirs='fnirs_cw_amplitude')
```

**Verification:**
```python
assert 'fnirs_cw_amplitude' in raw
```

### Step 12: 'fnirs_raw' in raw

```python
'fnirs_raw' in raw
```

**Verification:**
```python
assert 'fnirs_od' not in raw
```


## Complete Example

```python
# Workflow
'Test reading NIRX files.'
raw = read_raw_nirx(fname_nirx_15_2, preload=True)
assert raw._data.shape == (64, 67)
assert raw.info['sfreq'] == 3.90625
assert raw.info['meas_date'] == dt.datetime(2019, 10, 2, 9, 8, 47, 511000, tzinfo=dt.timezone.utc)
assert raw.info['ch_names'][:4] == ['S1_D1 760', 'S1_D1 850', 'S1_D10 760', 'S1_D10 850']
assert raw.info['subject_info'] == dict(sex=1, first_name='TestRecording', birthday=dt.date(1989, 10, 2), his_id='TestRecording')
assert_array_equal(raw.annotations.description, ['4.0', '6.0', '2.0'])
print(raw.annotations.onset)
allowed_dist_error = 0.0002
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
mni_locs = apply_trans(head_mri_t, locs)
assert raw.info['ch_names'][0][3:5] == 'D1'
assert_allclose(mni_locs[0], [-0.0292, 0.0852, -0.0142], atol=allowed_dist_error)
assert raw.info['ch_names'][15][3:5] == 'D4'
assert_allclose(mni_locs[15], [-0.0739, -0.0756, -0.0075], atol=allowed_dist_error)
assert 'fnirs_cw_amplitude' in raw
with pytest.raises(ValueError, match='Invalid value'):
    'fnirs_raw' in raw
assert 'fnirs_od' not in raw
picks = pick_types(raw.info, fnirs='fnirs_cw_amplitude')
assert len(picks) > 0
```

## Next Steps


---

*Source: test_nirx.py:493 | Complexity: Advanced | Last updated: 2026-05-18*