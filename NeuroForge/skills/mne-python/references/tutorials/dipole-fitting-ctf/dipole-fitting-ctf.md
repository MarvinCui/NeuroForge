# How To: Dipole Fitting Ctf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test dipole fitting with CTF data.

## Prerequisites

**Required Modules:**
- `os`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.dipole`
- `mne.io`
- `mne.proj`
- `mne.simulation`
- `mne.surface`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test dipole fitting with CTF data.'

```python
'Test dipole fitting with CTF data.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Assign raw_ctf = read_raw_ctf.set_eeg_reference(...)

```python
raw_ctf = read_raw_ctf(fname_ctf).set_eeg_reference(projection=True)
```

### Step 4: Assign events = make_fixed_length_events(...)

```python
events = make_fixed_length_events(raw_ctf, 1)
```

### Step 5: Assign evoked = Epochs.average(...)

```python
evoked = Epochs(raw_ctf, events, 1, 0, 0, baseline=None).average()
```

### Step 6: Assign cov = make_ad_hoc_cov(...)

```python
cov = make_ad_hoc_cov(evoked.info)
```

### Step 7: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model((0.0, 0.0, 0.0))
```

### Step 8: Call fit_dipole()

```python
fit_dipole(evoked, cov, sphere, rank=dict(meg=len(evoked.data)), tol=0.001, accuracy='accurate')
```


## Complete Example

```python
# Workflow
'Test dipole fitting with CTF data.'
pytest.importorskip('nibabel')
raw_ctf = read_raw_ctf(fname_ctf).set_eeg_reference(projection=True)
events = make_fixed_length_events(raw_ctf, 1)
evoked = Epochs(raw_ctf, events, 1, 0, 0, baseline=None).average()
cov = make_ad_hoc_cov(evoked.info)
sphere = make_sphere_model((0.0, 0.0, 0.0))
fit_dipole(evoked, cov, sphere, rank=dict(meg=len(evoked.data)), tol=0.001, accuracy='accurate')
```

## Next Steps


---

*Source: test_dipole.py:101 | Complexity: Advanced | Last updated: 2026-05-18*