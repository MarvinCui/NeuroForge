# How To: Rap Music Picks

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test RAP-MUSIC with picking.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.beamformer`
- `mne.cov`
- `mne.datasets`
- `mne.minimum_norm.tests.test_inverse`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test RAP-MUSIC with picking.'

```python
'Test RAP-MUSIC with picking.'
```

**Verification:**
```python
assert len(dipoles) == 2
```

### Step 2: Assign evoked = mne.read_evokeds(...)

```python
evoked = mne.read_evokeds(fname_ave, condition='Right Auditory', baseline=(None, 0))
```

### Step 3: Call evoked.crop()

```python
evoked.crop(tmin=0.05, tmax=0.15)
```

### Step 4: Call evoked.pick()

```python
evoked.pick(picks='meg')
```

### Step 5: Assign forward = mne.read_forward_solution(...)

```python
forward = mne.read_forward_solution(fname_fwd)
```

### Step 6: Assign noise_cov = mne.read_cov(...)

```python
noise_cov = mne.read_cov(fname_cov)
```

### Step 7: Assign dipoles = rap_music(...)

```python
dipoles = rap_music(evoked, forward, noise_cov, n_dipoles=2)
```

**Verification:**
```python
assert len(dipoles) == 2
```


## Complete Example

```python
# Workflow
'Test RAP-MUSIC with picking.'
evoked = mne.read_evokeds(fname_ave, condition='Right Auditory', baseline=(None, 0))
evoked.crop(tmin=0.05, tmax=0.15)
evoked.pick(picks='meg')
forward = mne.read_forward_solution(fname_fwd)
noise_cov = mne.read_cov(fname_cov)
dipoles = rap_music(evoked, forward, noise_cov, n_dipoles=2)
assert len(dipoles) == 2
```

## Next Steps


---

*Source: test_rap_music.py:202 | Complexity: Intermediate | Last updated: 2026-05-18*