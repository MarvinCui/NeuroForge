# How To: Correction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Apply HFC and compare to previous computed solutions.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: order
```

## Step-by-Step Guide

### Step 1: 'Apply HFC and compare to previous computed solutions.'

```python
'Apply HFC and compare to previous computed solutions.'
```

**Verification:**
```python
assert_allclose(got, want, rtol=1e-07)
```

### Step 2: Assign binname = value

```python
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
```

**Verification:**
```python
assert 0.999999 < corr <= 1.0
```

### Step 3: Assign raw = read_raw_fil(...)

```python
raw = read_raw_fil(binname)
```

### Step 4: Call raw.load_data()

```python
raw.load_data()
```

### Step 5: Call unknown.extend()

```python
raw.info['bads'].extend([b for b in bads])
```

### Step 6: Assign projs = compute_proj_hfc(...)

```python
projs = compute_proj_hfc(raw.info, order=order, accuracy='point')
```

### Step 7: Call raw.add_proj.apply_proj()

```python
raw.add_proj(projs).apply_proj()
```

### Step 8: Assign mat = _unpack_mat(...)

```python
mat = _unpack_mat(loadmat(fil_path / f'{fname_root}_hfc_l{order}.mat'))
```

### Step 9: Assign proj_list = value

```python
proj_list = projs[0]['data']['col_names']
```

### Step 10: Assign picks = pick_channels(...)

```python
picks = pick_channels(raw.ch_names, proj_list, ordered=True)
```

### Step 11: Assign mat_list = value

```python
mat_list = mat['coil_label']
```

### Step 12: Assign mat_inds = pick_channels(...)

```python
mat_inds = pick_channels(mat_list, proj_list, ordered=True)
```

### Step 13: Assign want = value

```python
want = mat['trial'][mat_inds]
```

### Step 14: Assign got = value

```python
got = raw.copy().add_proj(projs).apply_proj()[picks, 0:300][0] * 1000000000000000.0
```

### Step 15: Call assert_allclose()

```python
assert_allclose(got, want, rtol=1e-07)
```

### Step 16: Assign projs = compute_proj_hfc(...)

```python
projs = compute_proj_hfc(raw.info, order=order)
```

### Step 17: Assign got = value

```python
got = raw.copy().add_proj(projs).apply_proj()[picks, 0:300][0] * 1000000000000000.0
```

### Step 18: Assign corr = value

```python
corr = np.corrcoef(got.ravel(), want.ravel())[0, 1]
```

**Verification:**
```python
assert 0.999999 < corr <= 1.0
```


## Complete Example

```python
# Setup
# Fixtures: order

# Workflow
'Apply HFC and compare to previous computed solutions.'
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
raw = read_raw_fil(binname)
raw.load_data()
raw.info['bads'].extend([b for b in bads])
projs = compute_proj_hfc(raw.info, order=order, accuracy='point')
raw.add_proj(projs).apply_proj()
mat = _unpack_mat(loadmat(fil_path / f'{fname_root}_hfc_l{order}.mat'))
proj_list = projs[0]['data']['col_names']
picks = pick_channels(raw.ch_names, proj_list, ordered=True)
mat_list = mat['coil_label']
mat_inds = pick_channels(mat_list, proj_list, ordered=True)
want = mat['trial'][mat_inds]
got = raw.copy().add_proj(projs).apply_proj()[picks, 0:300][0] * 1000000000000000.0
assert_allclose(got, want, rtol=1e-07)
projs = compute_proj_hfc(raw.info, order=order)
got = raw.copy().add_proj(projs).apply_proj()[picks, 0:300][0] * 1000000000000000.0
corr = np.corrcoef(got.ravel(), want.ravel())[0, 1]
assert 0.999999 < corr <= 1.0
```

## Next Steps


---

*Source: test_hfc.py:66 | Complexity: Advanced | Last updated: 2026-05-18*