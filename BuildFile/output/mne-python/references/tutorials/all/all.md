# How To: All

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test maxwell filter using all options.

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

### Step 1: 'Test maxwell filter using all options.'

```python
'Test maxwell filter using all options.'
```

**Verification:**
```python
assert_meg_snr(sss_py, sss_mf, mins[ii], meds[ii], msg=rf)
```

### Step 2: Assign raw_fnames = value

```python
raw_fnames = (raw_fname, raw_fname, erm_fname, sample_fname)
```

### Step 3: Assign sss_fnames = value

```python
sss_fnames = (sss_st1FineCalCrossTalkRegIn_fname, sss_st1FineCalCrossTalkRegInTransSample_fname, sss_erm_st1FineCalCrossTalkRegIn_fname, sss_samp_fname)
```

### Step 4: Assign fine_cals = value

```python
fine_cals = (fine_cal_fname, fine_cal_fname, fine_cal_fname, fine_cal_mgh_fname)
```

### Step 5: Assign coord_frames = value

```python
coord_frames = ('head', 'head', 'meg', 'head')
```

### Step 6: Assign ctcs = value

```python
ctcs = (ctc_fname, ctc_fname, ctc_fname, ctc_mgh_fname)
```

### Step 7: Assign mins = value

```python
mins = (3.5, 3.5, 1.2, 0.9)
```

### Step 8: Assign meds = value

```python
meds = (10.8, 10.2, 3.2, 5.9)
```

### Step 9: Assign st_durs = value

```python
st_durs = (1.0, 1.0, 1.0, None)
```

### Step 10: Assign destinations = value

```python
destinations = (None, sample_fname, None, None)
```

### Step 11: Assign origins = value

```python
origins = (mf_head_origin, mf_head_origin, mf_meg_origin, mf_head_origin)
```

### Step 12: Assign raw = read_crop(...)

```python
raw = read_crop(rf, (0.0, 1.0))
```

### Step 13: Assign sss_mf = read_crop(...)

```python
sss_mf = read_crop(sss_fnames[ii])
```

### Step 14: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, sss_mf, mins[ii], meds[ii], msg=rf)
```

### Step 15: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, calibration=fine_cals[ii], cross_talk=ctcs[ii], st_duration=st_durs[ii], coord_frame=coord_frames[ii], destination=destinations[ii], origin=origins[ii])
```


## Complete Example

```python
# Workflow
'Test maxwell filter using all options.'
raw_fnames = (raw_fname, raw_fname, erm_fname, sample_fname)
sss_fnames = (sss_st1FineCalCrossTalkRegIn_fname, sss_st1FineCalCrossTalkRegInTransSample_fname, sss_erm_st1FineCalCrossTalkRegIn_fname, sss_samp_fname)
fine_cals = (fine_cal_fname, fine_cal_fname, fine_cal_fname, fine_cal_mgh_fname)
coord_frames = ('head', 'head', 'meg', 'head')
ctcs = (ctc_fname, ctc_fname, ctc_fname, ctc_mgh_fname)
mins = (3.5, 3.5, 1.2, 0.9)
meds = (10.8, 10.2, 3.2, 5.9)
st_durs = (1.0, 1.0, 1.0, None)
destinations = (None, sample_fname, None, None)
origins = (mf_head_origin, mf_head_origin, mf_meg_origin, mf_head_origin)
for ii, rf in enumerate(raw_fnames):
    raw = read_crop(rf, (0.0, 1.0))
    with _record_warnings():
        sss_py = maxwell_filter(raw, calibration=fine_cals[ii], cross_talk=ctcs[ii], st_duration=st_durs[ii], coord_frame=coord_frames[ii], destination=destinations[ii], origin=origins[ii])
    sss_mf = read_crop(sss_fnames[ii])
    assert_meg_snr(sss_py, sss_mf, mins[ii], meds[ii], msg=rf)
```

## Next Steps


---

*Source: test_maxwell.py:1469 | Complexity: Advanced | Last updated: 2026-05-18*