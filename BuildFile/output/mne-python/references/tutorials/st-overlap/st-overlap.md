# How To: St Overlap

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test st_overlap.

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

### Step 1: 'Test st_overlap.'

```python
'Test st_overlap.'
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 2: Assign raw = read_crop.crop(...)

```python
raw = read_crop(raw_fname).crop(0, 1.0)
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 3: Assign mag_picks = pick_types(...)

```python
mag_picks = pick_types(raw.info, meg='mag', exclude=())
```

### Step 4: Assign power = np.sqrt(...)

```python
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
```

### Step 5: Assign kwargs = dict(...)

```python
kwargs = dict(origin=mf_head_origin, regularize=None, bad_condition='ignore', st_duration=0.5)
```

### Step 6: Assign raw_tsss = maxwell_filter(...)

```python
raw_tsss = maxwell_filter(raw, **kwargs)
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 7: Call _assert_shielding()

```python
_assert_shielding(raw_tsss, power, 35.8, max_factor=35.9)
```

### Step 8: Assign raw_tsss = _maxwell_filter_ola(...)

```python
raw_tsss = _maxwell_filter_ola(raw, st_overlap=True, **kwargs)
```

**Verification:**
```python
assert _compute_rank_int(raw_tsss, proj=False) == 140
```

### Step 9: Call _assert_shielding()

```python
_assert_shielding(raw_tsss, power, 35.6, max_factor=35.7)
```


## Complete Example

```python
# Workflow
'Test st_overlap.'
raw = read_crop(raw_fname).crop(0, 1.0)
mag_picks = pick_types(raw.info, meg='mag', exclude=())
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
kwargs = dict(origin=mf_head_origin, regularize=None, bad_condition='ignore', st_duration=0.5)
raw_tsss = maxwell_filter(raw, **kwargs)
assert _compute_rank_int(raw_tsss, proj=False) == 140
_assert_shielding(raw_tsss, power, 35.8, max_factor=35.9)
raw_tsss = _maxwell_filter_ola(raw, st_overlap=True, **kwargs)
assert _compute_rank_int(raw_tsss, proj=False) == 140
_assert_shielding(raw_tsss, power, 35.6, max_factor=35.7)
```

## Next Steps


---

*Source: test_maxwell.py:762 | Complexity: Advanced | Last updated: 2026-05-18*