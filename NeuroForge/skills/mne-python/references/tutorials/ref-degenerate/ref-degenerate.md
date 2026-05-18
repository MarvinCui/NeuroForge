# How To: Ref Degenerate

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reference channel handling and degenerate conditions.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.io`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.hfc`


## Step-by-Step Guide

### Step 1: 'Test reference channel handling and degenerate conditions.'

```python
'Test reference channel handling and degenerate conditions.'
```

**Verification:**
```python
assert len(projs) == 3
```

### Step 2: Assign info = read_info(...)

```python
info = read_info(ctf_fname)
```

**Verification:**
```python
assert projs[0]['desc'] == 'HFC: l=1 m=-1'
```

### Step 3: Assign projs = compute_proj_hfc(...)

```python
projs = compute_proj_hfc(info)
```

**Verification:**
```python
assert projs[1]['desc'] == 'HFC: l=1 m=0'
```

### Step 4: Assign meg_names = value

```python
meg_names = [info['ch_names'][pick] for pick in pick_types(info, meg=True, ref_meg=False, exclude=[])]
```

**Verification:**
```python
assert projs[2]['desc'] == 'HFC: l=1 m=1'
```

### Step 5: Assign meg_ref_names = value

```python
meg_ref_names = [info['ch_names'][pick] for pick in pick_types(info, meg=True, ref_meg=True, exclude=[])]
```

**Verification:**
```python
assert projs[0]['data']['col_names'] == meg_names
```

### Step 6: Assign projs = compute_proj_hfc(...)

```python
projs = compute_proj_hfc(info, picks=('meg', 'ref_meg'))
```

**Verification:**
```python
assert projs[0]['data']['col_names'] == meg_ref_names
```

### Step 7: Assign info = read_info(...)

```python
info = read_info(fif_fname)
```

### Step 8: Call compute_proj_hfc()

```python
compute_proj_hfc(info)
```

### Step 9: Assign unknown = value

```python
info['chs'][0]['loc'][:] = np.nan
```

### Step 10: Assign info_eeg = pick_info(...)

```python
info_eeg = pick_info(info, pick_types(info, meg=False, eeg=True))
```

### Step 11: Call compute_proj_hfc()

```python
compute_proj_hfc(info, picks=[0, 330])
```

### Step 12: Call compute_proj_hfc()

```python
compute_proj_hfc(info)
```

### Step 13: Call compute_proj_hfc()

```python
compute_proj_hfc(info_eeg)
```


## Complete Example

```python
# Workflow
'Test reference channel handling and degenerate conditions.'
info = read_info(ctf_fname)
projs = compute_proj_hfc(info)
meg_names = [info['ch_names'][pick] for pick in pick_types(info, meg=True, ref_meg=False, exclude=[])]
assert len(projs) == 3
assert projs[0]['desc'] == 'HFC: l=1 m=-1'
assert projs[1]['desc'] == 'HFC: l=1 m=0'
assert projs[2]['desc'] == 'HFC: l=1 m=1'
assert projs[0]['data']['col_names'] == meg_names
meg_ref_names = [info['ch_names'][pick] for pick in pick_types(info, meg=True, ref_meg=True, exclude=[])]
projs = compute_proj_hfc(info, picks=('meg', 'ref_meg'))
assert projs[0]['data']['col_names'] == meg_ref_names
info = read_info(fif_fname)
compute_proj_hfc(info)
with pytest.raises(ValueError, match='Only.*could be interpreted as MEG'):
    compute_proj_hfc(info, picks=[0, 330])
info['chs'][0]['loc'][:] = np.nan
with pytest.raises(ValueError, match='non-finite projectors'):
    compute_proj_hfc(info)
info_eeg = pick_info(info, pick_types(info, meg=False, eeg=True))
with pytest.raises(ValueError, match="picks \\(\\'meg\\'\\) could not be"):
    compute_proj_hfc(info_eeg)
```

## Next Steps


---

*Source: test_hfc.py:119 | Complexity: Advanced | Last updated: 2026-05-18*