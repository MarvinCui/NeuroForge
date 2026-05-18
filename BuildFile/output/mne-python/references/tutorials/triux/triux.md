# How To: Triux

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test TRIUX system support.

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

### Step 1: 'Test TRIUX system support.'

```python
'Test TRIUX system support.'
```

**Verification:**
```python
assert_allclose(raw.info['chs'][2]['cal'], 1.33e-10, rtol=1e-06)
```

### Step 2: Assign raw = read_crop(...)

```python
raw = read_crop(tri_fname, (0, 0.999))
```

**Verification:**
```python
assert_meg_snr(sss_py, read_crop(tri_sss_fname), 37, 700)
```

### Step 3: Call _assert_mag_coil_type()

```python
_assert_mag_coil_type(raw.info, FIFF.FIFFV_COIL_VV_MAG_T1)
```

**Verification:**
```python
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_fname), 31, 250)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(raw.info['chs'][2]['cal'], 1.33e-10, rtol=1e-06)
```

**Verification:**
```python
assert_meg_snr(sss_py, read_crop(tri_sss_cal_fname), 5, 100)
```

### Step 5: Call _assert_mag_coil_type()

```python
_assert_mag_coil_type(sss_py.info, FIFF.FIFFV_COIL_VV_MAG_T3)
```

**Verification:**
```python
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_cal_fname), 5, 100)
```

### Step 6: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, read_crop(tri_sss_fname), 37, 700)
```

**Verification:**
```python
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
```

### Step 7: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, cross_talk=tri_ctc_fname)
```

**Verification:**
```python
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
```

### Step 8: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_fname), 31, 250)
```

**Verification:**
```python
assert_meg_snr(sss_py, read_crop(tri_sss_st4_fname), 700.0, 1600)
```

### Step 9: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, calibration=tri_cal_fname)
```

### Step 10: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, read_crop(tri_sss_cal_fname), 5, 100)
```

### Step 11: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, calibration=tri_cal_fname, cross_talk=tri_ctc_fname)
```

### Step 12: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_cal_fname), 5, 100)
```

### Step 13: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize='in')
```

### Step 14: Assign sss_mf = read_crop(...)

```python
sss_mf = read_crop(tri_sss_reg_fname)
```

### Step 15: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
```

### Step 16: Call _check_reg_match()

```python
_check_reg_match(sss_py, sss_mf, 1)
```

### Step 17: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize='in', calibration=tri_cal_fname, cross_talk=tri_ctc_fname)
```

### Step 18: Assign sss_mf = read_crop(...)

```python
sss_mf = read_crop(tri_sss_ctc_cal_reg_in_fname)
```

### Step 19: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
```

### Step 20: Call _check_reg_match()

```python
_check_reg_match(sss_py, sss_mf, 1)
```

### Step 21: Assign raw = read_crop.fix_mag_coil_types(...)

```python
raw = read_crop(tri_fname).fix_mag_coil_types()
```

### Step 22: Call assert_meg_snr()

```python
assert_meg_snr(sss_py, read_crop(tri_sss_st4_fname), 700.0, 1600)
```

### Step 23: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None)
```

### Step 24: Assign sss_py = maxwell_filter(...)

```python
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, st_duration=4.0, verbose=True)
```


## Complete Example

```python
# Workflow
'Test TRIUX system support.'
raw = read_crop(tri_fname, (0, 0.999))
_assert_mag_coil_type(raw.info, FIFF.FIFFV_COIL_VV_MAG_T1)
assert_allclose(raw.info['chs'][2]['cal'], 1.33e-10, rtol=1e-06)
with use_coil_def(elekta_def_fname):
    sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None)
_assert_mag_coil_type(sss_py.info, FIFF.FIFFV_COIL_VV_MAG_T3)
assert_meg_snr(sss_py, read_crop(tri_sss_fname), 37, 700)
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, cross_talk=tri_ctc_fname)
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_fname), 31, 250)
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, calibration=tri_cal_fname)
assert_meg_snr(sss_py, read_crop(tri_sss_cal_fname), 5, 100)
sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, calibration=tri_cal_fname, cross_talk=tri_ctc_fname)
assert_meg_snr(sss_py, read_crop(tri_sss_ctc_cal_fname), 5, 100)
sss_py = maxwell_filter(raw, coord_frame='meg', regularize='in')
sss_mf = read_crop(tri_sss_reg_fname)
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
_check_reg_match(sss_py, sss_mf, 1)
sss_py = maxwell_filter(raw, coord_frame='meg', regularize='in', calibration=tri_cal_fname, cross_talk=tri_ctc_fname)
sss_mf = read_crop(tri_sss_ctc_cal_reg_in_fname)
assert_meg_snr(sss_py, sss_mf, 0.6, 9)
_check_reg_match(sss_py, sss_mf, 1)
raw = read_crop(tri_fname).fix_mag_coil_types()
with use_coil_def(elekta_def_fname):
    sss_py = maxwell_filter(raw, coord_frame='meg', regularize=None, st_duration=4.0, verbose=True)
assert_meg_snr(sss_py, read_crop(tri_sss_st4_fname), 700.0, 1600)
```

## Next Steps


---

*Source: test_maxwell.py:1504 | Complexity: Advanced | Last updated: 2026-05-18*