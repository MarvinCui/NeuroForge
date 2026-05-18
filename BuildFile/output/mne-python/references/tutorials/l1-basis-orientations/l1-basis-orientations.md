# How To: L1 Basis Orientations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that angles between the basis components matches orientations.

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

### Step 1: 'Test that angles between the basis components matches orientations.'

```python
'Test that angles between the basis components matches orientations.'
```

**Verification:**
```python
assert len(picks) == 68
```

### Step 2: Assign binname = value

```python
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
```

**Verification:**
```python
assert basis.shape == (len(picks), 3)
```

### Step 3: Assign raw = read_raw_fil(...)

```python
raw = read_raw_fil(binname)
```

**Verification:**
```python
assert ang_model.shape == (n_ang,)
```

### Step 4: Call unknown.extend()

```python
raw.info['bads'].extend([b for b in bads])
```

**Verification:**
```python
assert ori_sens.shape == (len(picks), 3)
```

### Step 5: Assign projs = compute_proj_hfc(...)

```python
projs = compute_proj_hfc(raw.info, accuracy='point')
```

**Verification:**
```python
assert ang_sens.shape == (n_ang,)
```

### Step 6: Assign basis = np.hstack(...)

```python
basis = np.hstack([p['data']['data'].T for p in projs])
```

**Verification:**
```python
assert_allclose(ang_sens, ang_model, atol=1e-07)
```

### Step 7: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg='mag')
```

**Verification:**
```python
assert len(picks) == 68
```

### Step 8: Assign ang_model = _angle_between_each(...)

```python
ang_model = _angle_between_each(basis)
```

### Step 9: Assign n_ang = value

```python
n_ang = len(picks) ** 2
```

**Verification:**
```python
assert ang_model.shape == (n_ang,)
```

### Step 10: Assign chs = value

```python
chs = pick_info(raw.info, picks)['chs']
```

### Step 11: Assign ori_sens = np.array(...)

```python
ori_sens = np.array([ch['loc'][-3:] for ch in chs])
```

**Verification:**
```python
assert ori_sens.shape == (len(picks), 3)
```

### Step 12: Assign ang_sens = _angle_between_each(...)

```python
ang_sens = _angle_between_each(ori_sens)
```

**Verification:**
```python
assert ang_sens.shape == (n_ang,)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(ang_sens, ang_model, atol=1e-07)
```


## Complete Example

```python
# Workflow
'Test that angles between the basis components matches orientations.'
binname = fil_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
raw = read_raw_fil(binname)
raw.info['bads'].extend([b for b in bads])
projs = compute_proj_hfc(raw.info, accuracy='point')
basis = np.hstack([p['data']['data'].T for p in projs])
picks = pick_types(raw.info, meg='mag')
assert len(picks) == 68
assert basis.shape == (len(picks), 3)
ang_model = _angle_between_each(basis)
n_ang = len(picks) ** 2
assert ang_model.shape == (n_ang,)
chs = pick_info(raw.info, picks)['chs']
ori_sens = np.array([ch['loc'][-3:] for ch in chs])
ori_sens /= np.linalg.norm(ori_sens, axis=0, keepdims=True)
assert ori_sens.shape == (len(picks), 3)
ang_sens = _angle_between_each(ori_sens)
assert ang_sens.shape == (n_ang,)
assert_allclose(ang_sens, ang_model, atol=1e-07)
```

## Next Steps


---

*Source: test_hfc.py:94 | Complexity: Advanced | Last updated: 2026-05-18*