# How To: Nirsport V2

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test NIRSport2 file.

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

### Step 1: 'Test NIRSport2 file.'

```python
'Test NIRSport2 file.'
```

**Verification:**
```python
assert raw._data.shape == (40, 128)
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(nirsport2, preload=True)
```

**Verification:**
```python
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.0304], atol=allowed_distance_error)
```

### Step 3: Assign allowed_distance_error = 0.005

```python
allowed_distance_error = 0.005
```

**Verification:**
```python
assert_allclose(source_detector_distances(raw.copy().pick('S2_D2 760').info), [0.04], atol=allowed_distance_error)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.0304], atol=allowed_distance_error)
```

**Verification:**
```python
assert raw.info['ch_names'][0][3:5] == 'D1'
```

### Step 5: Call assert_allclose()

```python
assert_allclose(source_detector_distances(raw.copy().pick('S2_D2 760').info), [0.04], atol=allowed_distance_error)
```

**Verification:**
```python
assert_allclose(mni_locs[0], [-0.0841, -0.0464, -0.0129], atol=allowed_dist_error)
```

### Step 6: Assign allowed_dist_error = 0.0002

```python
allowed_dist_error = 0.0002
```

**Verification:**
```python
assert raw.info['ch_names'][2][3:5] == 'D6'
```

### Step 7: Assign locs = value

```python
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
```

**Verification:**
```python
assert_allclose(mni_locs[2], [-0.0841, -0.0138, 0.0248], atol=allowed_dist_error)
```

### Step 8: Assign unknown = _get_trans(...)

```python
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
```

**Verification:**
```python
assert raw.info['ch_names'][34][3:5] == 'D5'
```

### Step 9: Assign mni_locs = apply_trans(...)

```python
mni_locs = apply_trans(head_mri_t, locs)
```

**Verification:**
```python
assert_allclose(mni_locs[34], [0.0845, -0.0451, -0.0123], atol=allowed_dist_error)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(mni_locs[0], [-0.0841, -0.0464, -0.0129], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.info['ch_names'][0][:2] == 'S1'
```

### Step 11: Call assert_allclose()

```python
assert_allclose(mni_locs[2], [-0.0841, -0.0138, 0.0248], atol=allowed_dist_error)
```

**Verification:**
```python
assert_allclose(mni_locs[0], [-0.0848, -0.0162, -0.0163], atol=allowed_dist_error)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(mni_locs[34], [0.0845, -0.0451, -0.0123], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.info['ch_names'][9][:2] == 'S2'
```

### Step 13: Assign locs = value

```python
locs = [ch['loc'][3:6] for ch in raw.info['chs']]
```

**Verification:**
```python
assert_allclose(mni_locs[9], [-0.0, -0.1195, 0.0142], atol=allowed_dist_error)
```

### Step 14: Assign unknown = _get_trans(...)

```python
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
```

**Verification:**
```python
assert raw.info['ch_names'][39][:2] == 'S8'
```

### Step 15: Assign mni_locs = apply_trans(...)

```python
mni_locs = apply_trans(head_mri_t, locs)
```

**Verification:**
```python
assert_allclose(mni_locs[34], [0.0828, -0.046, 0.0285], atol=allowed_dist_error)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(mni_locs[0], [-0.0848, -0.0162, -0.0163], atol=allowed_dist_error)
```

**Verification:**
```python
assert len(raw.annotations) == 3
```

### Step 17: Call assert_allclose()

```python
assert_allclose(mni_locs[9], [-0.0, -0.1195, 0.0142], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.annotations.description[0] == '1.0'
```

### Step 18: Call assert_allclose()

```python
assert_allclose(mni_locs[34], [0.0828, -0.046, 0.0285], atol=allowed_dist_error)
```

**Verification:**
```python
assert raw.annotations.description[2] == '6.0'
```

### Step 19: Call assert_allclose()

```python
assert_allclose(np.diff(raw.annotations.onset), [2.3, 3.1], atol=0.1)
```

**Verification:**
```python
assert_allclose(np.diff(raw.annotations.onset), [2.3, 3.1], atol=0.1)
```

### Step 20: Assign mon = raw.get_montage(...)

```python
mon = raw.get_montage()
```

**Verification:**
```python
assert len(mon.dig) == 27
```


## Complete Example

```python
# Workflow
'Test NIRSport2 file.'
raw = read_raw_nirx(nirsport2, preload=True)
assert raw._data.shape == (40, 128)
allowed_distance_error = 0.005
assert_allclose(source_detector_distances(raw.copy().pick('S1_D1 760').info), [0.0304], atol=allowed_distance_error)
assert_allclose(source_detector_distances(raw.copy().pick('S2_D2 760').info), [0.04], atol=allowed_distance_error)
allowed_dist_error = 0.0002
locs = [ch['loc'][6:9] for ch in raw.info['chs']]
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
mni_locs = apply_trans(head_mri_t, locs)
assert raw.info['ch_names'][0][3:5] == 'D1'
assert_allclose(mni_locs[0], [-0.0841, -0.0464, -0.0129], atol=allowed_dist_error)
assert raw.info['ch_names'][2][3:5] == 'D6'
assert_allclose(mni_locs[2], [-0.0841, -0.0138, 0.0248], atol=allowed_dist_error)
assert raw.info['ch_names'][34][3:5] == 'D5'
assert_allclose(mni_locs[34], [0.0845, -0.0451, -0.0123], atol=allowed_dist_error)
locs = [ch['loc'][3:6] for ch in raw.info['chs']]
head_mri_t, _ = _get_trans('fsaverage', 'head', 'mri')
mni_locs = apply_trans(head_mri_t, locs)
assert raw.info['ch_names'][0][:2] == 'S1'
assert_allclose(mni_locs[0], [-0.0848, -0.0162, -0.0163], atol=allowed_dist_error)
assert raw.info['ch_names'][9][:2] == 'S2'
assert_allclose(mni_locs[9], [-0.0, -0.1195, 0.0142], atol=allowed_dist_error)
assert raw.info['ch_names'][39][:2] == 'S8'
assert_allclose(mni_locs[34], [0.0828, -0.046, 0.0285], atol=allowed_dist_error)
assert len(raw.annotations) == 3
assert raw.annotations.description[0] == '1.0'
assert raw.annotations.description[2] == '6.0'
assert_allclose(np.diff(raw.annotations.onset), [2.3, 3.1], atol=0.1)
mon = raw.get_montage()
assert len(mon.dig) == 27
```

## Next Steps


---

*Source: test_nirx.py:80 | Complexity: Advanced | Last updated: 2026-05-18*