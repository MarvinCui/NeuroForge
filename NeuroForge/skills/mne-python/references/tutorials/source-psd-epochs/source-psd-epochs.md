# How To: Source Psd Epochs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test multi-taper source PSD computation in label from epochs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.minimum_norm.time_frequency`
- `mne.time_frequency.multitaper`

**Setup Required:**
```python
# Fixtures: method
```

## Step-by-Step Guide

### Step 1: 'Test multi-taper source PSD computation in label from epochs.'

```python
'Test multi-taper source PSD computation in label from epochs.'
```

**Verification:**
```python
assert_allclose(stc_psd.data, stc_psd_gen.data, atol=1e-07)
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname_data)
```

**Verification:**
```python
assert_allclose(psd, stc_psd.data, atol=1e-07)
```

### Step 3: Assign inverse_operator = read_inverse_operator(...)

```python
inverse_operator = read_inverse_operator(fname_inv)
```

**Verification:**
```python
assert_allclose(freqs, stc_psd.times)
```

### Step 4: Assign label = read_label(...)

```python
label = read_label(fname_label)
```

### Step 5: Assign label2 = read_label(...)

```python
label2 = read_label(fname_label2)
```

### Step 6: Assign unknown = value

```python
event_id, tmin, tmax = (1, -0.2, 0.5)
```

### Step 7: Assign lambda2 = value

```python
lambda2 = 1.0 / 9.0
```

### Step 8: Assign bandwidth = 8.0

```python
bandwidth = 8.0
```

### Step 9: Assign unknown = value

```python
fmin, fmax = (0, 100)
```

### Step 10: Assign picks = pick_types(...)

```python
picks = pick_types(raw.info, meg=True, eeg=False, stim=True, ecg=True, eog=True, include=['STI 014'], exclude='bads')
```

### Step 11: Assign reject = dict(...)

```python
reject = dict(grad=4e-10, mag=4e-12, eog=0.00015)
```

### Step 12: Assign events = find_events(...)

```python
events = find_events(raw, stim_channel='STI 014')
```

### Step 13: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), reject=reject)
```

### Step 14: Call epochs.drop_bad()

```python
epochs.drop_bad()
```

### Step 15: Assign one_epochs = value

```python
one_epochs = epochs[:1]
```

### Step 16: Assign inv = prepare_inverse_operator(...)

```python
inv = prepare_inverse_operator(inverse_operator, nave=1, lambda2=1.0 / 9.0, method='dSPM')
```

### Step 17: Assign stc_psd = value

```python
stc_psd = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, prepared=True)[0]
```

### Step 18: Assign stcs = compute_source_psd_epochs(...)

```python
stcs = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, return_generator=True, prepared=True)
```

### Step 19: Call assert_allclose()

```python
assert_allclose(stc_psd.data, stc_psd_gen.data, atol=1e-07)
```

### Step 20: Assign stc = value

```python
stc = apply_inverse_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, prepared=True)[0]
```

### Step 21: Assign sfreq = value

```python
sfreq = epochs.info['sfreq']
```

### Step 22: Assign unknown = psd_array_multitaper(...)

```python
psd, freqs = psd_array_multitaper(stc.data, sfreq=sfreq, bandwidth=bandwidth, fmin=fmin, fmax=fmax)
```

### Step 23: Call assert_allclose()

```python
assert_allclose(psd, stc_psd.data, atol=1e-07)
```

### Step 24: Call assert_allclose()

```python
assert_allclose(freqs, stc_psd.times)
```

### Step 25: Assign stc_psd_gen = stc

```python
stc_psd_gen = stc
```

### Step 26: Call compute_source_psd_epochs()

```python
compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=0.01, low_bias=True, fmin=fmin, fmax=fmax, return_generator=False, prepared=True)
```

### Step 27: Call compute_source_psd_epochs()

```python
compute_source_psd_epochs(one_epochs, inv, label=[label, label2])
```


## Complete Example

```python
# Setup
# Fixtures: method

# Workflow
'Test multi-taper source PSD computation in label from epochs.'
raw = read_raw_fif(fname_data)
inverse_operator = read_inverse_operator(fname_inv)
label = read_label(fname_label)
label2 = read_label(fname_label2)
event_id, tmin, tmax = (1, -0.2, 0.5)
lambda2 = 1.0 / 9.0
bandwidth = 8.0
fmin, fmax = (0, 100)
picks = pick_types(raw.info, meg=True, eeg=False, stim=True, ecg=True, eog=True, include=['STI 014'], exclude='bads')
reject = dict(grad=4e-10, mag=4e-12, eog=0.00015)
events = find_events(raw, stim_channel='STI 014')
epochs = Epochs(raw, events, event_id, tmin, tmax, picks=picks, baseline=(None, 0), reject=reject)
epochs.drop_bad()
one_epochs = epochs[:1]
inv = prepare_inverse_operator(inverse_operator, nave=1, lambda2=1.0 / 9.0, method='dSPM')
stc_psd = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, prepared=True)[0]
stcs = compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=bandwidth, fmin=fmin, fmax=fmax, return_generator=True, prepared=True)
for stc in stcs:
    stc_psd_gen = stc
assert_allclose(stc_psd.data, stc_psd_gen.data, atol=1e-07)
stc = apply_inverse_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, prepared=True)[0]
sfreq = epochs.info['sfreq']
psd, freqs = psd_array_multitaper(stc.data, sfreq=sfreq, bandwidth=bandwidth, fmin=fmin, fmax=fmax)
assert_allclose(psd, stc_psd.data, atol=1e-07)
assert_allclose(freqs, stc_psd.times)
with pytest.raises(ValueError, match='use a value of at least'):
    compute_source_psd_epochs(one_epochs, inv, lambda2=lambda2, method=method, pick_ori='normal', label=label, bandwidth=0.01, low_bias=True, fmin=fmin, fmax=fmax, return_generator=False, prepared=True)
with pytest.raises(TypeError, match='Label or BiHemi'):
    compute_source_psd_epochs(one_epochs, inv, label=[label, label2])
```

## Next Steps


---

*Source: test_time_frequency.py:341 | Complexity: Advanced | Last updated: 2026-05-18*