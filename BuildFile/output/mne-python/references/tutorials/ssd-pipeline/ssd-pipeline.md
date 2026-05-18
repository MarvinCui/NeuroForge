# How To: Ssd Pipeline

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if SSD works in a pipeline.

## Prerequisites

**Required Modules:**
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.pipeline`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne._fiff.pick`
- `mne.decoding`
- `mne.decoding._mod_ged`
- `mne.decoding.ssd`
- `mne.filter`
- `mne.time_frequency`


## Step-by-Step Guide

### Step 1: 'Test if SSD works in a pipeline.'

```python
'Test if SSD works in a pipeline.'
```

**Verification:**
```python
assert out.shape == (100, 2)
```

### Step 2: Assign sf = 250

```python
sf = 250
```

**Verification:**
```python
assert pipe.get_params()['SSD__n_components'] == 5
```

### Step 3: Assign unknown = simulate_data(...)

```python
X, A, S = simulate_data(n_trials=100, n_channels=20, n_samples=500)
```

### Step 4: Assign X_e = np.reshape(...)

```python
X_e = np.reshape(X, (100, 20, 500))
```

### Step 5: Assign y = np.random.RandomState.randint(...)

```python
y = np.random.RandomState(0).randint(2, size=100)
```

### Step 6: Assign info = create_info(...)

```python
info = create_info(ch_names=20, sfreq=sf, ch_types='eeg')
```

### Step 7: Assign filt_params_signal = dict(...)

```python
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 8: Assign filt_params_noise = dict(...)

```python
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
```

### Step 9: Assign ssd = SSD(...)

```python
ssd = SSD(info, filt_params_signal, filt_params_noise)
```

### Step 10: Assign csp = CSP(...)

```python
csp = CSP()
```

### Step 11: Assign pipe = Pipeline(...)

```python
pipe = Pipeline([('SSD', ssd), ('CSP', csp)])
```

### Step 12: Call pipe.set_params()

```python
pipe.set_params(SSD__n_components=5)
```

### Step 13: Call pipe.set_params()

```python
pipe.set_params(CSP__n_components=2)
```

### Step 14: Assign out = pipe.fit_transform(...)

```python
out = pipe.fit_transform(X_e, y)
```

**Verification:**
```python
assert out.shape == (100, 2)
```


## Complete Example

```python
# Workflow
'Test if SSD works in a pipeline.'
sf = 250
X, A, S = simulate_data(n_trials=100, n_channels=20, n_samples=500)
X_e = np.reshape(X, (100, 20, 500))
y = np.random.RandomState(0).randint(2, size=100)
info = create_info(ch_names=20, sfreq=sf, ch_types='eeg')
filt_params_signal = dict(l_freq=freqs_sig[0], h_freq=freqs_sig[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
filt_params_noise = dict(l_freq=freqs_noise[0], h_freq=freqs_noise[1], l_trans_bandwidth=4, h_trans_bandwidth=4)
ssd = SSD(info, filt_params_signal, filt_params_noise)
csp = CSP()
pipe = Pipeline([('SSD', ssd), ('CSP', csp)])
pipe.set_params(SSD__n_components=5)
pipe.set_params(CSP__n_components=2)
out = pipe.fit_transform(X_e, y)
assert out.shape == (100, 2)
assert pipe.get_params()['SSD__n_components'] == 5
```

## Next Steps


---

*Source: test_ssd.py:332 | Complexity: Advanced | Last updated: 2026-05-18*