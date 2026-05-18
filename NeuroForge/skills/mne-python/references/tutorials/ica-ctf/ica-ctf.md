# How To: Ica Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test run ICA computation on ctf data with/without compensation.

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `scipy.io`
- `mne`
- `mne._fiff.pick`
- `mne.cov`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.io.eeglab.eeglab`
- `mne.preprocessing`
- `mne.preprocessing`
- `mne.preprocessing.ica`
- `mne.rank`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test run ICA computation on ctf data with/without compensation.'

```python
'Test run ICA computation on ctf data with/without compensation.'
```

### Step 2: Assign method = 'fastica'

```python
method = 'fastica'
```

### Step 3: Assign raw = read_raw_ctf.crop.load_data(...)

```python
raw = read_raw_ctf(ctf_fname).crop(0, 3).load_data()
```

### Step 4: Assign picks = sorted(...)

```python
picks = sorted(set(range(0, len(raw.ch_names), 10)) | set(pick_types(raw.info, ref_meg=True)))
```

### Step 5: Call raw.pick()

```python
raw.pick(picks)
```

### Step 6: Assign events = make_fixed_length_events(...)

```python
events = make_fixed_length_events(raw, 99999)
```

### Step 7: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(0)
```

### Step 8: Assign ica = ICA(...)

```python
ica = ICA(n_components=2, max_iter=2, method=method)
```

### Step 9: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

### Step 10: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(1)
```

### Step 11: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events=events, tmin=-0.2, tmax=0.2, baseline=None, preload=True)
```

### Step 12: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 13: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(comp)
```

### Step 14: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, events=events, tmin=-0.2, tmax=0.2, baseline=None, preload=True)
```

### Step 15: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 16: Call ica.fit()

```python
ica.fit(raw)
```

### Step 17: Assign ica = ICA(...)

```python
ica = ICA(n_components=2, max_iter=2, method=method)
```

### Step 18: Call _assert_ica_attributes()

```python
_assert_ica_attributes(ica)
```

### Step 19: Call ica.apply()

```python
ica.apply(inst.copy())
```

### Step 20: Call ica.get_sources()

```python
ica.get_sources(inst)
```

### Step 21: Call ica.apply()

```python
ica.apply(inst.copy())
```

### Step 22: Call ica.get_sources()

```python
ica.get_sources(inst)
```

### Step 23: Call ica.fit()

```python
ica.fit(inst)
```


## Complete Example

```python
# Workflow
'Test run ICA computation on ctf data with/without compensation.'
method = 'fastica'
raw = read_raw_ctf(ctf_fname).crop(0, 3).load_data()
picks = sorted(set(range(0, len(raw.ch_names), 10)) | set(pick_types(raw.info, ref_meg=True)))
raw.pick(picks)
events = make_fixed_length_events(raw, 99999)
for comp in [0, 1]:
    raw.apply_gradient_compensation(comp)
    epochs = Epochs(raw, events=events, tmin=-0.2, tmax=0.2, baseline=None, preload=True)
    evoked = epochs.average()
    for inst in [raw, epochs]:
        ica = ICA(n_components=2, max_iter=2, method=method)
        with _record_warnings():
            ica.fit(inst)
        _assert_ica_attributes(ica)
    for inst in [raw, epochs, evoked]:
        ica.apply(inst.copy())
        ica.get_sources(inst)
raw.apply_gradient_compensation(0)
ica = ICA(n_components=2, max_iter=2, method=method)
with _record_warnings():
    ica.fit(raw)
_assert_ica_attributes(ica)
raw.apply_gradient_compensation(1)
epochs = Epochs(raw, events=events, tmin=-0.2, tmax=0.2, baseline=None, preload=True)
evoked = epochs.average()
for inst in [raw, epochs, evoked]:
    with pytest.raises(RuntimeError, match='Compensation grade of ICA'):
        ica.apply(inst.copy())
    with pytest.raises(RuntimeError, match='Compensation grade of ICA'):
        ica.get_sources(inst)
```

## Next Steps


---

*Source: test_ica.py:1406 | Complexity: Advanced | Last updated: 2026-05-18*