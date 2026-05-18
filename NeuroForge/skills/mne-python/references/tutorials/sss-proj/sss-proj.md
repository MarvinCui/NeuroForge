# How To: Sss Proj

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test `meg` proj option.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff.proj`
- `mne.cov`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.proj`
- `mne.rank`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test `meg` proj option.'

```python
'Test `meg` proj option.'
```

**Verification:**
```python
assert len(raw_sss.info['projs']) == 0
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert len(this_raw.info['projs']) == n_proj
```

### Step 3: Call raw.crop.load_data.pick()

```python
raw.crop(0, 1.0).load_data().pick(picks='meg')
```

**Verification:**
```python
assert ch_names == this_raw.ch_names
```

### Step 4: Call raw.pick.del_proj()

```python
raw.pick(raw.ch_names[:51]).del_proj()
```

**Verification:**
```python
assert want_rank == sss_proj_rank == rank
```

### Step 5: Assign raw_sss = maxwell_filter(...)

```python
raw_sss = maxwell_filter(raw, int_order=5, ext_order=2)
```

**Verification:**
```python
assert this_raw.info['projs'][0]['data']['col_names'] == ch_names
```

### Step 6: Assign sss_rank = 21

```python
sss_rank = 21
```

**Verification:**
```python
assert this_raw.info['projs'][3]['data']['col_names'] == mag_names
```

### Step 7: Assign proj = compute_proj_raw(...)

```python
proj = compute_proj_raw(raw_sss, n_grad=3, n_mag=3, meg=meg, verbose='error')
```

### Step 8: Assign this_raw = raw_sss.copy.add_proj.apply_proj(...)

```python
this_raw = raw_sss.copy().add_proj(proj).apply_proj()
```

**Verification:**
```python
assert len(this_raw.info['projs']) == n_proj
```

### Step 9: Assign sss_proj_rank = _compute_rank_int(...)

```python
sss_proj_rank = _compute_rank_int(this_raw)
```

### Step 10: Assign cov = compute_raw_covariance(...)

```python
cov = compute_raw_covariance(this_raw, verbose='error')
```

### Step 11: Assign unknown = compute_whitener(...)

```python
W, ch_names, rank = compute_whitener(cov, this_raw.info, return_rank=True)
```

**Verification:**
```python
assert ch_names == this_raw.ch_names
```

### Step 12: Assign mag_names = value

```python
mag_names = ch_names[2::3]
```

**Verification:**
```python
assert this_raw.info['projs'][3]['data']['col_names'] == mag_names
```


## Complete Example

```python
# Workflow
'Test `meg` proj option.'
raw = read_raw_fif(raw_fname)
raw.crop(0, 1.0).load_data().pick(picks='meg')
raw.pick(raw.ch_names[:51]).del_proj()
raw_sss = maxwell_filter(raw, int_order=5, ext_order=2)
sss_rank = 21
assert len(raw_sss.info['projs']) == 0
for meg, n_proj, want_rank in (('separate', 6, sss_rank), ('combined', 3, sss_rank - 3)):
    proj = compute_proj_raw(raw_sss, n_grad=3, n_mag=3, meg=meg, verbose='error')
    this_raw = raw_sss.copy().add_proj(proj).apply_proj()
    assert len(this_raw.info['projs']) == n_proj
    sss_proj_rank = _compute_rank_int(this_raw)
    cov = compute_raw_covariance(this_raw, verbose='error')
    W, ch_names, rank = compute_whitener(cov, this_raw.info, return_rank=True)
    assert ch_names == this_raw.ch_names
    assert want_rank == sss_proj_rank == rank
    if meg == 'combined':
        assert this_raw.info['projs'][0]['data']['col_names'] == ch_names
    else:
        mag_names = ch_names[2::3]
        assert this_raw.info['projs'][3]['data']['col_names'] == mag_names
```

## Next Steps


---

*Source: test_proj.py:506 | Complexity: Advanced | Last updated: 2026-05-18*