# How To: Proj Raw Duration

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test equivalence of `duration` options.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: duration, sfreq
```

## Step-by-Step Guide

### Step 1: 'Test equivalence of `duration` options.'

```python
'Test equivalence of `duration` options.'
```

**Verification:**
```python
assert len(proj_dur) == len(proj_none) == len(proj_def) == n_dim
```

### Step 2: Assign unknown = value

```python
n_ch, n_dim = (30, 3)
```

**Verification:**
```python
assert_allclose(pu['data']['data'], pn['data']['data'])
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert angle < 1e-05
```

### Step 4: Assign signals = rng.randn(...)

```python
signals = rng.randn(n_dim, 10000)
```

### Step 5: Assign mixing = value

```python
mixing = rng.randn(n_ch, n_dim) + [0, 1, 2]
```

### Step 6: Assign data = np.dot(...)

```python
data = np.dot(mixing, signals)
```

### Step 7: Assign raw = RawArray(...)

```python
raw = RawArray(data, create_info(n_ch, sfreq, 'eeg'))
```

### Step 8: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference(projection=True)
```

### Step 9: Assign n_eff = int(...)

```python
n_eff = int(round(raw.info['sfreq'] * duration))
```

### Step 10: Assign stop = value

```python
stop = (len(raw.times) // n_eff * n_eff - 1) / raw.info['sfreq']
```

### Step 11: Call raw.crop()

```python
raw.crop(0, stop)
```

### Step 12: Assign proj_def = compute_proj_raw(...)

```python
proj_def = compute_proj_raw(raw, n_eeg=n_dim)
```

### Step 13: Assign proj_dur = compute_proj_raw(...)

```python
proj_dur = compute_proj_raw(raw, duration=duration, n_eeg=n_dim)
```

### Step 14: Assign proj_none = compute_proj_raw(...)

```python
proj_none = compute_proj_raw(raw, duration=None, n_eeg=n_dim)
```

**Verification:**
```python
assert len(proj_dur) == len(proj_none) == len(proj_def) == n_dim
```

### Step 15: Call assert_allclose()

```python
assert_allclose(pu['data']['data'], pn['data']['data'])
```

### Step 16: Assign computed = np.concatenate(...)

```python
computed = np.concatenate([p['data']['data'] for p in proj], 0)
```

### Step 17: Assign angle = np.rad2deg(...)

```python
angle = np.rad2deg(linalg.subspace_angles(computed.T, mixing)[0])
```

**Verification:**
```python
assert angle < 1e-05
```


## Complete Example

```python
# Setup
# Fixtures: duration, sfreq

# Workflow
'Test equivalence of `duration` options.'
n_ch, n_dim = (30, 3)
rng = np.random.RandomState(0)
signals = rng.randn(n_dim, 10000)
mixing = rng.randn(n_ch, n_dim) + [0, 1, 2]
data = np.dot(mixing, signals)
raw = RawArray(data, create_info(n_ch, sfreq, 'eeg'))
raw.set_eeg_reference(projection=True)
n_eff = int(round(raw.info['sfreq'] * duration))
stop = (len(raw.times) // n_eff * n_eff - 1) / raw.info['sfreq']
raw.crop(0, stop)
proj_def = compute_proj_raw(raw, n_eeg=n_dim)
proj_dur = compute_proj_raw(raw, duration=duration, n_eeg=n_dim)
proj_none = compute_proj_raw(raw, duration=None, n_eeg=n_dim)
assert len(proj_dur) == len(proj_none) == len(proj_def) == n_dim
for pu, pn in zip(proj_dur, proj_none):
    assert_allclose(pu['data']['data'], pn['data']['data'])
for proj in (proj_dur, proj_none, proj_def):
    computed = np.concatenate([p['data']['data'] for p in proj], 0)
    angle = np.rad2deg(linalg.subspace_angles(computed.T, mixing)[0])
    assert angle < 1e-05
```

## Next Steps


---

*Source: test_proj.py:334 | Complexity: Advanced | Last updated: 2026-05-18*