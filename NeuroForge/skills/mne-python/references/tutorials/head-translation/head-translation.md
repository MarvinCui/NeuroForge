# How To: Head Translation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test Maxwell filter head translation.

## Prerequisites

**Required Modules:**
- `pathlib`
- `re`
- `contextlib`
- `functools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.chpi`
- `mne.datasets`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.maxwell`
- `mne.rank`
- `mne.utils`
- `scipy.io`


## Step-by-Step Guide

### Step 1: 'Test Maxwell filter head translation.'

```python
'Test Maxwell filter head translation.'
```

**Verification:**
```python
assert_meg_snr(raw_sss, read_crop(sss_std_fname, (0.0, 1.0)), 200.0)
```

### Step 2: Assign raw = read_crop(...)

```python
raw = read_crop(raw_fname, (0.0, 1.0))
```

**Verification:**
```python
assert_meg_snr(raw_sss, read_crop(sss_trans_default_fname), 125.0)
```

### Step 3: Call assert_meg_snr()

```python
assert_meg_snr(raw_sss, read_crop(sss_std_fname, (0.0, 1.0)), 200.0)
```

**Verification:**
```python
assert_allclose(raw_sss.info['dev_head_t']['trans'], destination)
```

### Step 4: Call assert_meg_snr()

```python
assert_meg_snr(raw_sss, read_crop(sss_trans_default_fname), 125.0)
```

**Verification:**
```python
assert_meg_snr(raw_sss, read_crop(sss_trans_sample_fname), 13.0, 100.0)
```

### Step 5: Assign destination = np.eye(...)

```python
destination = np.eye(4)
```

**Verification:**
```python
assert_allclose(raw_sss.info['dev_head_t']['trans'], read_info(sample_fname)['dev_head_t']['trans'])
```

### Step 6: Assign unknown = 0.04

```python
destination[2, 3] = 0.04
```

### Step 7: Call assert_allclose()

```python
assert_allclose(raw_sss.info['dev_head_t']['trans'], destination)
```

### Step 8: Call assert_meg_snr()

```python
assert_meg_snr(raw_sss, read_crop(sss_trans_sample_fname), 13.0, 100.0)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(raw_sss.info['dev_head_t']['trans'], read_info(sample_fname)['dev_head_t']['trans'])
```

### Step 10: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, destination=raw_fname, origin=mf_head_origin, regularize=None, bad_condition='ignore')
```

### Step 11: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, destination=str(sample_fname), origin=mf_head_origin, regularize=None, bad_condition='ignore', verbose=True)
```

### Step 12: Call maxwell_filter()

```python
maxwell_filter(raw, destination=mf_head_origin, coord_frame='meg')
```

### Step 13: Call maxwell_filter()

```python
maxwell_filter(raw, destination=[0.0] * 4)
```

### Step 14: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, destination=mf_head_origin, origin=mf_head_origin, regularize=None, bad_condition='ignore', verbose=True)
```


## Complete Example

```python
# Workflow
'Test Maxwell filter head translation.'
raw = read_crop(raw_fname, (0.0, 1.0))
with use_coil_def(elekta_def_fname):
    raw_sss = maxwell_filter(raw, destination=raw_fname, origin=mf_head_origin, regularize=None, bad_condition='ignore')
assert_meg_snr(raw_sss, read_crop(sss_std_fname, (0.0, 1.0)), 200.0)
with use_coil_def(elekta_def_fname):
    with pytest.warns(RuntimeWarning, match='over 25 mm'):
        raw_sss = maxwell_filter(raw, destination=mf_head_origin, origin=mf_head_origin, regularize=None, bad_condition='ignore', verbose=True)
assert_meg_snr(raw_sss, read_crop(sss_trans_default_fname), 125.0)
destination = np.eye(4)
destination[2, 3] = 0.04
assert_allclose(raw_sss.info['dev_head_t']['trans'], destination)
with pytest.warns(RuntimeWarning, match='= 25.6 mm'):
    raw_sss = maxwell_filter(raw, destination=str(sample_fname), origin=mf_head_origin, regularize=None, bad_condition='ignore', verbose=True)
assert_meg_snr(raw_sss, read_crop(sss_trans_sample_fname), 13.0, 100.0)
assert_allclose(raw_sss.info['dev_head_t']['trans'], read_info(sample_fname)['dev_head_t']['trans'])
with pytest.raises(RuntimeError, match='.* can only be set .* head .*'):
    maxwell_filter(raw, destination=mf_head_origin, coord_frame='meg')
with pytest.raises(ValueError, match='destination must be'):
    maxwell_filter(raw, destination=[0.0] * 4)
```

## Next Steps


---

*Source: test_maxwell.py:1012 | Complexity: Advanced | Last updated: 2026-05-18*