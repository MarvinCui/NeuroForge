# How To: Spatiotemporal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test Maxwell filter (tSSS) spatiotemporal processing.

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

### Step 1: 'Test Maxwell filter (tSSS) spatiotemporal processing.'

```python
'Test Maxwell filter (tSSS) spatiotemporal processing.'
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 2: Assign raw = read_crop(...)

```python
raw = read_crop(raw_fname)
```

**Verification:**
```python
assert_meg_snr(raw_tsss, tsss_bench, *tol)
```

### Step 3: Assign mag_picks = pick_types(...)

```python
mag_picks = pick_types(raw.info, meg='mag', exclude=())
```

**Verification:**
```python
assert len(py_st) > 0
```

### Step 4: Assign power = np.sqrt(...)

```python
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
```

**Verification:**
```python
assert py_st['buflen'] == st_duration
```

### Step 5: Assign st_durations = value

```python
st_durations = [4.0]
```

**Verification:**
```python
assert py_st['subspcorr'] == 0.98
```

### Step 6: Assign tols = value

```python
tols = [(80, 100)]
```

### Step 7: Assign kwargs = dict(...)

```python
kwargs = dict(origin=mf_head_origin, regularize=None, bad_condition='ignore')
```

### Step 8: Call maxwell_filter()

```python
maxwell_filter(raw, st_duration=1000.0)
```

### Step 9: Assign tSSS_fname = value

```python
tSSS_fname = sss_path / f'test_move_anon_st{int(st_duration)}s_raw_sss.fif'
```

### Step 10: Assign tsss_bench = read_crop(...)

```python
tsss_bench = read_crop(tSSS_fname)
```

### Step 11: Assign raw_tsss = maxwell_filter(...)

```python
raw_tsss = maxwell_filter(raw, st_duration=st_duration, **kwargs)
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 12: Call assert_meg_snr()

```python
assert_meg_snr(raw_tsss, tsss_bench, *tol)
```

### Step 13: Assign py_st = value

```python
py_st = raw_tsss.info['proc_history'][0]['max_info']['max_st']
```

**Verification:**
```python
assert len(py_st) > 0
```

### Step 14: Call _assert_shielding()

```python
_assert_shielding(raw_tsss, power, 20.8)
```

### Step 15: Call maxwell_filter()

```python
maxwell_filter(raw, st_duration=10.0, st_correlation=0.0)
```


## Complete Example

```python
# Workflow
'Test Maxwell filter (tSSS) spatiotemporal processing.'
raw = read_crop(raw_fname)
mag_picks = pick_types(raw.info, meg='mag', exclude=())
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
with pytest.raises(ValueError, match='must be'):
    maxwell_filter(raw, st_duration=1000.0)
st_durations = [4.0]
tols = [(80, 100)]
kwargs = dict(origin=mf_head_origin, regularize=None, bad_condition='ignore')
for st_duration, tol in zip(st_durations, tols):
    tSSS_fname = sss_path / f'test_move_anon_st{int(st_duration)}s_raw_sss.fif'
    tsss_bench = read_crop(tSSS_fname)
    raw_tsss = maxwell_filter(raw, st_duration=st_duration, **kwargs)
    assert _compute_rank_int(raw_tsss, proj=False) == 140
    assert_meg_snr(raw_tsss, tsss_bench, *tol)
    py_st = raw_tsss.info['proc_history'][0]['max_info']['max_st']
    assert len(py_st) > 0
    assert py_st['buflen'] == st_duration
    assert py_st['subspcorr'] == 0.98
    _assert_shielding(raw_tsss, power, 20.8)
with pytest.raises(ValueError, match='Need 0 < st_correlation'):
    maxwell_filter(raw, st_duration=10.0, st_correlation=0.0)
```

## Next Steps


---

*Source: test_maxwell.py:715 | Complexity: Advanced | Last updated: 2026-05-18*