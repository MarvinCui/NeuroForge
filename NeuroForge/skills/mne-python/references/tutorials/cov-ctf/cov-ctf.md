# How To: Cov Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test basic cov computation on ctf data with/without compensation.

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `inspect`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.cov`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.preprocessing`
- `mne.rank`
- `mne.utils`
- `sklearn`


## Step-by-Step Guide

### Step 1: 'Test basic cov computation on ctf data with/without compensation.'

```python
'Test basic cov computation on ctf data with/without compensation.'
```

**Verification:**
```python
assert len(events) == 2
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert raw.info['comps'], 'Comps matrices removed'
```

### Step 3: Assign raw = read_raw_ctf.crop.load_data(...)

```python
raw = read_raw_ctf(ctf_fname).crop(0.0, 2.0).load_data()
```

### Step 4: Assign events = make_fixed_length_events(...)

```python
events = make_fixed_length_events(raw, 99999)
```

**Verification:**
```python
assert len(events) == 2
```

### Step 5: Assign ch_names = value

```python
ch_names = [raw.info['ch_names'][pick] for pick in pick_types(raw.info, meg=True, eeg=False, ref_meg=False)]
```

### Step 6: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(0)
```

### Step 7: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, -0.2, 0.2, preload=True)
```

### Step 8: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(1)
```

**Verification:**
```python
assert raw.info['comps'], 'Comps matrices removed'
```

### Step 9: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(comp)
```

### Step 10: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events, None, -0.2, 0.2, preload=True)
```

### Step 11: Assign noise_cov = compute_covariance(...)

```python
noise_cov = compute_covariance(epochs, tmax=0.0, method=['empirical'])
```

### Step 12: Call prepare_noise_cov()

```python
prepare_noise_cov(noise_cov, raw.info, ch_names)
```

### Step 13: Assign noise_cov = compute_covariance(...)

```python
noise_cov = compute_covariance(epochs, tmax=0.0, method=['empirical'])
```

### Step 14: Call prepare_noise_cov()

```python
prepare_noise_cov(noise_cov, raw.info, ch_names)
```


## Complete Example

```python
# Workflow
'Test basic cov computation on ctf data with/without compensation.'
pytest.importorskip('sklearn')
raw = read_raw_ctf(ctf_fname).crop(0.0, 2.0).load_data()
events = make_fixed_length_events(raw, 99999)
assert len(events) == 2
ch_names = [raw.info['ch_names'][pick] for pick in pick_types(raw.info, meg=True, eeg=False, ref_meg=False)]
for comp in [0, 1]:
    raw.apply_gradient_compensation(comp)
    epochs = Epochs(raw, events, None, -0.2, 0.2, preload=True)
    with _record_warnings(), pytest.warns(RuntimeWarning, match='Too few samples'):
        noise_cov = compute_covariance(epochs, tmax=0.0, method=['empirical'])
    with pytest.warns(RuntimeWarning, match='orders of magnitude'):
        prepare_noise_cov(noise_cov, raw.info, ch_names)
raw.apply_gradient_compensation(0)
epochs = Epochs(raw, events, None, -0.2, 0.2, preload=True)
with _record_warnings(), pytest.warns(RuntimeWarning, match='Too few samples'):
    noise_cov = compute_covariance(epochs, tmax=0.0, method=['empirical'])
raw.apply_gradient_compensation(1)
with pytest.warns(RuntimeWarning, match='orders of magnitude'):
    prepare_noise_cov(noise_cov, raw.info, ch_names)
assert raw.info['comps'], 'Comps matrices removed'
```

## Next Steps


---

*Source: test_cov.py:901 | Complexity: Advanced | Last updated: 2026-05-18*