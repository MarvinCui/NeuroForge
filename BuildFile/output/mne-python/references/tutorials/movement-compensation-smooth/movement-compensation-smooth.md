# How To: Movement Compensation Smooth

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test movement compensation with smooth interpolation.

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

### Step 1: 'Test movement compensation with smooth interpolation.'

```python
'Test movement compensation with smooth interpolation.'
```

**Verification:**
```python
assert want_re.match(log) is not None, log
```

### Step 2: Assign lims = value

```python
lims = (0, 10)
```

**Verification:**
```python
assert want_re.match(log) is not None, log
```

### Step 3: Assign raw = read_crop.load_data(...)

```python
raw = read_crop(raw_fname, lims).load_data()
```

### Step 4: Assign mag_picks = pick_types(...)

```python
mag_picks = pick_types(raw.info, meg='mag', exclude=())
```

### Step 5: Assign power = np.sqrt(...)

```python
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
```

### Step 6: Assign head_pos = read_head_pos(...)

```python
head_pos = read_head_pos(pos_fname)
```

### Step 7: Assign kwargs = dict(...)

```python
kwargs = dict(head_pos=head_pos, origin=mf_head_origin, regularize=None, bad_condition='ignore')
```

### Step 8: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, **kwargs)
```

### Step 9: Call _assert_shielding()

```python
_assert_shielding(raw_sss, power, 0.258, max_factor=0.259)
```

### Step 10: Assign raw_sss_smooth = _maxwell_filter_ola(...)

```python
raw_sss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', **kwargs)
```

### Step 11: Call _assert_shielding()

```python
_assert_shielding(raw_sss_smooth, raw_sss, 1.01, max_factor=1.02)
```

### Step 12: Assign unknown = 'in'

```python
kwargs['regularize'] = 'in'
```

### Step 13: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, **kwargs)
```

### Step 14: Call _assert_shielding()

```python
_assert_shielding(raw_sss, power, 0.84, max_factor=0.85)
```

### Step 15: Assign raw_sss_smooth = _maxwell_filter_ola(...)

```python
raw_sss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', **kwargs)
```

### Step 16: Call _assert_shielding()

```python
_assert_shielding(raw_sss_smooth, raw_sss, 1.008, max_factor=1.012)
```

### Step 17: Assign unknown = 10

```python
kwargs['st_duration'] = 10
```

### Step 18: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

### Step 19: Assign want_re = re.compile(...)

```python
want_re = re.compile('.*Projecting 25 intersecting.*across 24 pos.*', re.DOTALL)
```

**Verification:**
```python
assert want_re.match(log) is not None, log
```

### Step 20: Call _assert_shielding()

```python
_assert_shielding(raw_tsss, power, 31.2, max_factor=31.3)
```

### Step 21: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert want_re.match(log) is not None, log
```

### Step 22: Call _assert_shielding()

```python
_assert_shielding(raw_tsss_smooth, power, 31.5, max_factor=31.7)
```

### Step 23: Assign raw_tsss = maxwell_filter(...)

```python
raw_tsss = maxwell_filter(raw, verbose=True, **kwargs)
```

### Step 24: Assign raw_tsss_smooth = _maxwell_filter_ola(...)

```python
raw_tsss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', st_overlap=True, verbose=True, **kwargs)
```


## Complete Example

```python
# Workflow
'Test movement compensation with smooth interpolation.'
lims = (0, 10)
raw = read_crop(raw_fname, lims).load_data()
mag_picks = pick_types(raw.info, meg='mag', exclude=())
power = np.sqrt(np.sum(raw[mag_picks][0] ** 2))
head_pos = read_head_pos(pos_fname)
kwargs = dict(head_pos=head_pos, origin=mf_head_origin, regularize=None, bad_condition='ignore')
raw_sss = maxwell_filter(raw, **kwargs)
_assert_shielding(raw_sss, power, 0.258, max_factor=0.259)
raw_sss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', **kwargs)
_assert_shielding(raw_sss_smooth, raw_sss, 1.01, max_factor=1.02)
kwargs['regularize'] = 'in'
raw_sss = maxwell_filter(raw, **kwargs)
_assert_shielding(raw_sss, power, 0.84, max_factor=0.85)
raw_sss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', **kwargs)
_assert_shielding(raw_sss_smooth, raw_sss, 1.008, max_factor=1.012)
kwargs['st_duration'] = 10
with catch_logging() as log:
    raw_tsss = maxwell_filter(raw, verbose=True, **kwargs)
log = log.getvalue()
want_re = re.compile('.*Projecting 25 intersecting.*across 24 pos.*', re.DOTALL)
assert want_re.match(log) is not None, log
_assert_shielding(raw_tsss, power, 31.2, max_factor=31.3)
with catch_logging() as log:
    raw_tsss_smooth = _maxwell_filter_ola(raw, mc_interp='hann', st_overlap=True, verbose=True, **kwargs)
log = log.getvalue()
assert want_re.match(log) is not None, log
_assert_shielding(raw_tsss_smooth, power, 31.5, max_factor=31.7)
```

## Next Steps


---

*Source: test_maxwell.py:316 | Complexity: Advanced | Last updated: 2026-05-18*