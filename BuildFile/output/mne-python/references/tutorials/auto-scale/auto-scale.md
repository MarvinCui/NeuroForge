# How To: Auto Scale

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test auto-scaling of channels for quick plotting.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `cycler`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.viz`
- `mne.viz.ui_events`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test auto-scaling of channels for quick plotting.'

```python
'Test auto-scaling of channels for quick plotting.'
```

**Verification:**
```python
assert scale_grad == scalings_new['grad']
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(raw_fname)
```

**Verification:**
```python
assert scalings_new['eeg'] != 'auto'
```

### Step 3: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw, read_events(ev_fname))
```

**Verification:**
```python
assert scalings_new['stim'] > 0
```

### Step 4: Assign rand_data = np.random.randn(...)

```python
rand_data = np.random.randn(10, 100)
```

### Step 5: Assign ix = raw.get_channel_types.index(...)

```python
ix = raw.get_channel_types().index('stim')
```

### Step 6: Call raw.load_data()

```python
raw.load_data()
```

### Step 7: Assign unknown = 0.0

```python
raw._data[ix] = 0.0
```

### Step 8: Assign epochs = unknown.load_data(...)

```python
epochs = epochs[0].load_data()
```

### Step 9: Call epochs.pick()

```python
epochs.pick(picks='eeg')
```

### Step 10: Assign scale_grad = 10000000000.0

```python
scale_grad = 10000000000.0
```

### Step 11: Assign scalings_def = dict(...)

```python
scalings_def = dict([('eeg', 'auto'), ('grad', scale_grad), ('stim', 'auto')])
```

### Step 12: Assign scalings_new = _compute_scalings(...)

```python
scalings_new = _compute_scalings(scalings_def, inst)
```

**Verification:**
```python
assert scale_grad == scalings_new['grad']
```

### Step 13: Call _compute_scalings()

```python
_compute_scalings(scalings_def, rand_data)
```

### Step 14: Call inst.plot()

```python
inst.plot(scalings='foo')
```


## Complete Example

```python
# Workflow
'Test auto-scaling of channels for quick plotting.'
raw = read_raw_fif(raw_fname)
epochs = Epochs(raw, read_events(ev_fname))
rand_data = np.random.randn(10, 100)
ix = raw.get_channel_types().index('stim')
raw.load_data()
raw._data[ix] = 0.0
for inst in [raw, epochs]:
    scale_grad = 10000000000.0
    scalings_def = dict([('eeg', 'auto'), ('grad', scale_grad), ('stim', 'auto')])
    with pytest.raises(ValueError, match=".*scalings.*'foo'.*"):
        inst.plot(scalings='foo')
    scalings_new = _compute_scalings(scalings_def, inst)
    assert scale_grad == scalings_new['grad']
    assert scalings_new['eeg'] != 'auto'
    assert scalings_new['stim'] > 0
with pytest.raises(ValueError, match='Must supply either Raw or Epochs'):
    _compute_scalings(scalings_def, rand_data)
epochs = epochs[0].load_data()
epochs.pick(picks='eeg')
```

## Next Steps


---

*Source: test_utils.py:127 | Complexity: Advanced | Last updated: 2026-05-18*