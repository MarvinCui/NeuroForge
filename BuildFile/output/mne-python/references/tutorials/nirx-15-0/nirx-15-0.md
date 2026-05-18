# How To: Nirx 15 0

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
assert raw._data.shape == (20, 92)
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname_nirx_15_0, preload=True)
```

**Verification:**
```python
assert raw.info['sfreq'] == 6.25
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(raw.annotations.description, ['1.0', '2.0', '2.0'])
```

**Verification:**
```python
assert raw.info['meas_date'] == dt.datetime(2019, 10, 27, 13, 53, 34, 209000, tzinfo=dt.timezone.utc)
```

### Step 4: Assign allowed_dist_error = 0.0002

```python
allowed_dist_error = 0.0002
```

**Verification:**
```python
assert raw.info['ch_names'][:12] == ['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850', 'S3_D3 760', 'S3_D3 850', 'S4_D4 760', 'S4_D4 850', 'S5_D5 760', 'S5_D5 850', 'S6_D6 760', 'S6_D6 850']
```

### Step 5: Assign locs = value

```python
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
```

**Verification:**
```python
assert raw.info['subject_info'] == {'birthday': dt.date(2004, 10, 27), 'first_name': 'NIRX', 'last_name': 'Test', 'sex': FIFF.FIFFV_SUBJ_SEX_UNKNOWN, 'his_id': 'NIRX_Test'}
```

### Step 6: Assign unknown = _get_trans(...)

```python
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
```

**Verification:**
```python
assert_array_equal(raw.annotations.description, ['1.0', '2.0', '2.0'])
```

### Step 7: Assign mni_locs = apply_trans(...)

```python
mni_locs = apply_trans(head_mri_t, locs)
```

**Verification:**
```python
assert raw.info['ch_names'][0][3:5] == 'D1'
```

### Step 8: Call assert_allclose()

```python
assert_allclose(mni_locs[0], [0.0287, -0.1143, -0.0332], atol=allowed_dist_error)
```

**Verification:**
```python
assert_allclose(mni_locs[0], [0.0287, -0.1143, -0.0332], atol=allowed_dist_error)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(mni_locs[15], [-0.0693, -0.048, 0.0657], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.info['ch_names'][15][3:5] == 'D8'
```

### Step 10: Assign allowed_distance_error = 0.0002

```python
allowed_distance_error = 0.0002
```

**Verification:**
```python
assert_allclose(mni_locs[15], [-0.0693, -0.048, 0.0657], atol=allowed_dist_error)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.03], atol=allowed_distance_error)
```

**Verification:**
```python
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.03], atol=allowed_distance_error)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(source_detector_distances(raw.copy().pick('S7_D7 760').info), [0.0392], atol=allowed_distance_error)
```

**Verification:**
```python
assert_allclose(source_detector_distances(raw.copy().pick('S7_D7 760').info), [0.0392], atol=allowed_distance_error)
```


## Complete Example

```python
# Workflow
'Test reading NIRX files.'
raw = read_raw_nirx(fname_nirx_15_0, preload=True)
assert raw._data.shape == (20, 92)
assert raw.info['sfreq'] == 6.25
assert raw.info['meas_date'] == dt.datetime(2019, 10, 27, 13, 53, 34, 209000, tzinfo=dt.timezone.utc)
assert raw.info['ch_names'][:12] == ['S1_D1 760', 'S1_D1 850', 'S2_D2 760', 'S2_D2 850', 'S3_D3 760', 'S3_D3 850', 'S4_D4 760', 'S4_D4 850', 'S5_D5 760', 'S5_D5 850', 'S6_D6 760', 'S6_D6 850']
assert raw.info['subject_info'] == {'birthday': dt.date(2004, 10, 27), 'first_name': 'NIRX', 'last_name': 'Test', 'sex': FIFF.FIFFV_SUBJ_SEX_UNKNOWN, 'his_id': 'NIRX_Test'}
assert_array_equal(raw.annotations.description, ['1.0', '2.0', '2.0'])
allowed_dist_error = 0.0002
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
mni_locs = apply_trans(head_mri_t, locs)
assert raw.info['ch_names'][0][3:5] == 'D1'
assert_allclose(mni_locs[0], [0.0287, -0.1143, -0.0332], atol=allowed_dist_error)
assert raw.info['ch_names'][15][3:5] == 'D8'
assert_allclose(mni_locs[15], [-0.0693, -0.048, 0.0657], atol=allowed_dist_error)
allowed_distance_error = 0.0002
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.03], atol=allowed_distance_error)
assert_allclose(source_detector_distances(raw.copy().pick('S7_D7 760').info), [0.0392], atol=allowed_distance_error)
```

## Next Steps


---

*Source: test_nirx.py:555 | Complexity: Advanced | Last updated: 2026-05-18*