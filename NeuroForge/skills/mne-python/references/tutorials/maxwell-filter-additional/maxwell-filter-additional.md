# How To: Maxwell Filter Additional

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test processing of Maxwell filtered data.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test processing of Maxwell filtered data.'

```python
'Test processing of Maxwell filtered data.'
```

**Verification:**
```python
assert_allclose(raw_sss_loaded[:][0], raw_sss[:][0], rtol=1e-06, atol=1e-20)
```

### Step 2: Assign file_name = 'test_move_anon'

```python
file_name = 'test_move_anon'
```

**Verification:**
```python
assert cov_raw_rank == raw.info['nchan']
```

### Step 3: Assign raw_fname = value

```python
raw_fname = data_path / 'SSS' / (file_name + '_raw.fif')
```

**Verification:**
```python
assert cov_sss_rank == _get_n_moments(int_order)
```

### Step 4: Assign raw = read_crop(...)

```python
raw = read_crop(raw_fname, (0.0, 2.0))
```

### Step 5: Call raw.load_data()

```python
raw.load_data()
```

### Step 6: Call raw.pick()

```python
raw.pick('meg')
```

### Step 7: Assign int_order = 8

```python
int_order = 8
```

### Step 8: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, origin=mf_head_origin, regularize=None, bad_condition='ignore')
```

### Step 9: Assign test_outname = value

```python
test_outname = tmp_path / 'test_raw_sss.fif'
```

### Step 10: Call raw_sss.save()

```python
raw_sss.save(test_outname)
```

### Step 11: Assign raw_sss_loaded = read_crop.load_data(...)

```python
raw_sss_loaded = read_crop(test_outname).load_data()
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw_sss_loaded[:][0], raw_sss[:][0], rtol=1e-06, atol=1e-20)
```

### Step 13: Assign cov_raw = compute_raw_covariance(...)

```python
cov_raw = compute_raw_covariance(raw)
```

### Step 14: Assign cov_sss = compute_raw_covariance(...)

```python
cov_sss = compute_raw_covariance(raw_sss)
```

### Step 15: Assign scalings = None

```python
scalings = None
```

### Step 16: Assign cov_raw_rank = _compute_rank_int(...)

```python
cov_raw_rank = _compute_rank_int(cov_raw, scalings=scalings, info=raw.info, proj=False)
```

### Step 17: Assign cov_sss_rank = _compute_rank_int(...)

```python
cov_sss_rank = _compute_rank_int(cov_sss, scalings=scalings, info=raw_sss.info, proj=False)
```

**Verification:**
```python
assert cov_raw_rank == raw.info['nchan']
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test processing of Maxwell filtered data.'
file_name = 'test_move_anon'
raw_fname = data_path / 'SSS' / (file_name + '_raw.fif')
raw = read_crop(raw_fname, (0.0, 2.0))
raw.load_data()
raw.pick('meg')
int_order = 8
raw_sss = maxwell_filter(raw, origin=mf_head_origin, regularize=None, bad_condition='ignore')
test_outname = tmp_path / 'test_raw_sss.fif'
raw_sss.save(test_outname)
raw_sss_loaded = read_crop(test_outname).load_data()
assert_allclose(raw_sss_loaded[:][0], raw_sss[:][0], rtol=1e-06, atol=1e-20)
cov_raw = compute_raw_covariance(raw)
cov_sss = compute_raw_covariance(raw_sss)
scalings = None
cov_raw_rank = _compute_rank_int(cov_raw, scalings=scalings, info=raw.info, proj=False)
cov_sss_rank = _compute_rank_int(cov_sss, scalings=scalings, info=raw_sss.info, proj=False)
assert cov_raw_rank == raw.info['nchan']
assert cov_sss_rank == _get_n_moments(int_order)
```

## Next Steps


---

*Source: test_maxwell.py:656 | Complexity: Advanced | Last updated: 2026-05-18*