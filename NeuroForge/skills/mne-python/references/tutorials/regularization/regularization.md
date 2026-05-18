# How To: Regularization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test Maxwell filter regularization.

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

### Step 1: 'Test Maxwell filter regularization.'

```python
'Test Maxwell filter regularization.'
```

**Verification:**
```python
assert_meg_snr(raw_sss, sss_reg_in, min_tols[ii], med_tols[ii], msg=rf)
```

### Step 2: Assign min_tols = value

```python
min_tols = (20.0, 2.6, 1.0)
```

### Step 3: Assign med_tols = value

```python
med_tols = (200.0, 21.0, 3.7)
```

### Step 4: Assign origins = value

```python
origins = ((0.0, 0.0, 0.04), (0.0,) * 3, (0.0, 0.02, 0.02))
```

### Step 5: Assign coord_frames = value

```python
coord_frames = ('head', 'meg', 'head')
```

### Step 6: Assign raw_fnames = value

```python
raw_fnames = (raw_fname, erm_fname, sample_fname)
```

### Step 7: Assign sss_fnames = value

```python
sss_fnames = (sss_reg_in_fname, sss_erm_reg_in_fname, sss_samp_reg_in_fname)
```

### Step 8: Assign comp_tols = value

```python
comp_tols = [0, 1, 4]
```

### Step 9: Assign raw = read_crop(...)

```python
raw = read_crop(rf, (0.0, 1.0))
```

### Step 10: Assign sss_reg_in = read_crop(...)

```python
sss_reg_in = read_crop(sss_fnames[ii])
```

### Step 11: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, coord_frame=coord_frames[ii], origin=origins[ii])
```

### Step 12: Call assert_meg_snr()

```python
assert_meg_snr(raw_sss, sss_reg_in, min_tols[ii], med_tols[ii], msg=rf)
```

### Step 13: Call _check_reg_match()

```python
_check_reg_match(raw_sss, sss_reg_in, comp_tols[ii])
```


## Complete Example

```python
# Workflow
'Test Maxwell filter regularization.'
min_tols = (20.0, 2.6, 1.0)
med_tols = (200.0, 21.0, 3.7)
origins = ((0.0, 0.0, 0.04), (0.0,) * 3, (0.0, 0.02, 0.02))
coord_frames = ('head', 'meg', 'head')
raw_fnames = (raw_fname, erm_fname, sample_fname)
sss_fnames = (sss_reg_in_fname, sss_erm_reg_in_fname, sss_samp_reg_in_fname)
comp_tols = [0, 1, 4]
for ii, rf in enumerate(raw_fnames):
    raw = read_crop(rf, (0.0, 1.0))
    sss_reg_in = read_crop(sss_fnames[ii])
    raw_sss = maxwell_filter(raw, coord_frame=coord_frames[ii], origin=origins[ii])
    assert_meg_snr(raw_sss, sss_reg_in, min_tols[ii], med_tols[ii], msg=rf)
    _check_reg_match(raw_sss, sss_reg_in, comp_tols[ii])
```

## Next Steps


---

*Source: test_maxwell.py:914 | Complexity: Advanced | Last updated: 2026-05-18*