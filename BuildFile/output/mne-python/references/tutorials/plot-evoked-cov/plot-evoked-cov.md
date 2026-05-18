# How To: Plot Evoked Cov

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_evoked with noise_cov.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.collections`
- `matplotlib.colors`
- `mpl_toolkits.axes_grid1.parasite_axes`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.stats.parametric`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plot_evoked with noise_cov.'

```python
'Test plot_evoked with noise_cov.'
```

### Step 2: Assign evoked = _get_epochs.average(...)

```python
evoked = _get_epochs().average()
```

### Step 3: Assign cov = read_cov(...)

```python
cov = read_cov(cov_fname)
```

### Step 4: Assign unknown = value

```python
cov['projs'] = []
```

### Step 5: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_sss_fname)
```

### Step 6: Assign events = make_fixed_length_events(...)

```python
events = make_fixed_length_events(raw)
```

### Step 7: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, picks=default_picks)
```

### Step 8: Assign cov = compute_covariance(...)

```python
cov = compute_covariance(epochs)
```

### Step 9: Assign evoked_sss = epochs.average(...)

```python
evoked_sss = epochs.average()
```

### Step 10: Call plt.close()

```python
plt.close('all')
```

### Step 11: Call evoked.plot()

```python
evoked.plot(noise_cov=cov, time_unit='s')
```

### Step 12: Call evoked.plot()

```python
evoked.plot(noise_cov=1.0, time_unit='s')
```

### Step 13: Call evoked.plot()

```python
evoked.plot(noise_cov='nonexistent-cov.fif', time_unit='s')
```

### Step 14: Call evoked_sss.plot()

```python
evoked_sss.plot(noise_cov=cov, time_unit='s')
```


## Complete Example

```python
# Workflow
'Test plot_evoked with noise_cov.'
evoked = _get_epochs().average()
cov = read_cov(cov_fname)
cov['projs'] = []
with pytest.warns(RuntimeWarning, match='No average EEG reference'):
    evoked.plot(noise_cov=cov, time_unit='s')
with pytest.raises(TypeError, match='Covariance'):
    evoked.plot(noise_cov=1.0, time_unit='s')
with pytest.raises(FileNotFoundError, match='File does not exist'):
    evoked.plot(noise_cov='nonexistent-cov.fif', time_unit='s')
raw = read_raw_fif(raw_sss_fname)
events = make_fixed_length_events(raw)
epochs = Epochs(raw, events, picks=default_picks)
cov = compute_covariance(epochs)
evoked_sss = epochs.average()
with _record_warnings(), pytest.warns(RuntimeWarning, match='relative scaling'):
    evoked_sss.plot(noise_cov=cov, time_unit='s')
plt.close('all')
```

## Next Steps


---

*Source: test_evoked.py:99 | Complexity: Advanced | Last updated: 2026-05-18*