# How To: Plot Volume Source Estimates On Vol Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot of source estimate on srcs setup on 2 labels.

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.minimum_norm`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plot of source estimate on srcs setup on 2 labels.'

```python
'Test plot of source estimate on srcs setup on 2 labels.'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

### Step 3: Call pytest.importorskip()

```python
pytest.importorskip('dipy')
```

### Step 4: Call pytest.importorskip()

```python
pytest.importorskip('nilearn')
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(data_dir / 'MEG' / 'sample' / 'sample_audvis_trunc_raw.fif', preload=False)
```

### Step 6: Call raw.pick.crop()

```python
raw.pick('meg').crop(0, 10)
```

### Step 7: Call raw.pick.del_proj.load_data()

```python
raw.pick(raw.ch_names[::2]).del_proj().load_data()
```

### Step 8: Assign epochs = make_fixed_length_epochs.apply_baseline(...)

```python
epochs = make_fixed_length_epochs(raw, preload=True).apply_baseline((None, None))
```

### Step 9: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 10: Assign subject = 'sample'

```python
subject = 'sample'
```

### Step 11: Assign bem = read_bem_solution(...)

```python
bem = read_bem_solution(subjects_dir / f'{subject}' / 'bem' / 'sample-320-bem-sol.fif')
```

### Step 12: Assign pos = 25.0

```python
pos = 25.0
```

### Step 13: Assign volume_label = value

```python
volume_label = ['Right-Cerebral-Cortex', 'Left-Cerebral-Cortex']
```

### Step 14: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(subject, subjects_dir=subjects_dir, pos=pos, mri=subjects_dir / subject / 'mri' / 'aseg.mgz', bem=bem, volume_label=volume_label, add_interpolator=False)
```

### Step 15: Assign trans = read_trans(...)

```python
trans = read_trans(data_dir / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif')
```

### Step 16: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(evoked.info, trans, src, bem, meg=True, eeg=False, mindist=0, n_jobs=1)
```

### Step 17: Assign cov = compute_covariance(...)

```python
cov = compute_covariance(epochs, tmin=None, tmax=None, method='empirical')
```

### Step 18: Assign inverse_operator = make_inverse_operator(...)

```python
inverse_operator = make_inverse_operator(evoked.info, fwd, cov, loose=1, depth=0.8)
```

### Step 19: Assign stc = apply_inverse(...)

```python
stc = apply_inverse(evoked, inverse_operator, 1.0 / 3 ** 2, method='sLORETA', pick_ori=None)
```

### Step 20: Call stc.plot()

```python
stc.plot(src, subject, subjects_dir, initial_time=0.03)
```


## Complete Example

```python
# Workflow
'Test plot of source estimate on srcs setup on 2 labels.'
pytest.importorskip('nibabel')
pytest.importorskip('dipy')
pytest.importorskip('nilearn')
raw = read_raw_fif(data_dir / 'MEG' / 'sample' / 'sample_audvis_trunc_raw.fif', preload=False)
raw.pick('meg').crop(0, 10)
raw.pick(raw.ch_names[::2]).del_proj().load_data()
epochs = make_fixed_length_epochs(raw, preload=True).apply_baseline((None, None))
evoked = epochs.average()
subject = 'sample'
bem = read_bem_solution(subjects_dir / f'{subject}' / 'bem' / 'sample-320-bem-sol.fif')
pos = 25.0
volume_label = ['Right-Cerebral-Cortex', 'Left-Cerebral-Cortex']
src = setup_volume_source_space(subject, subjects_dir=subjects_dir, pos=pos, mri=subjects_dir / subject / 'mri' / 'aseg.mgz', bem=bem, volume_label=volume_label, add_interpolator=False)
trans = read_trans(data_dir / 'MEG' / 'sample' / 'sample_audvis_trunc-trans.fif')
fwd = make_forward_solution(evoked.info, trans, src, bem, meg=True, eeg=False, mindist=0, n_jobs=1)
cov = compute_covariance(epochs, tmin=None, tmax=None, method='empirical')
inverse_operator = make_inverse_operator(evoked.info, fwd, cov, loose=1, depth=0.8)
stc = apply_inverse(evoked, inverse_operator, 1.0 / 3 ** 2, method='sLORETA', pick_ori=None)
stc.plot(src, subject, subjects_dir, initial_time=0.03)
```

## Next Steps


---

*Source: test_3d_mpl.py:157 | Complexity: Advanced | Last updated: 2026-05-18*