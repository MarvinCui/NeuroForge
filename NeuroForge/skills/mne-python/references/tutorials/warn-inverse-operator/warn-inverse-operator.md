# How To: Warn Inverse Operator

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test MNE inverse warning without average EEG projection.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `re`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.time_frequency`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: evoked, noise_cov
```

## Step-by-Step Guide

### Step 1: 'Test MNE inverse warning without average EEG projection.'

```python
'Test MNE inverse warning without average EEG projection.'
```

**Verification:**
```python
assert bad_info['bads'] == ['MEG 2443', 'EEG 053']
```

### Step 2: Assign bad_info = value

```python
bad_info = evoked.info
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 3: Assign data = value

```python
data = evoked.data
```

**Verification:**
```python
assert evoked_cust.info['custom_ref_applied']
```

### Step 4: Assign tmax = value

```python
tmax = evoked.tmax
```

**Verification:**
```python
assert 'eeg' in raw
```

### Step 5: Assign fwd_op = convert_forward_solution(...)

```python
fwd_op = convert_forward_solution(read_forward_solution(fname_fwd), surf_ori=True, copy=False)
```

**Verification:**
```python
assert 'meg' in raw
```

### Step 6: Call unknown.pop()

```python
noise_cov['projs'].pop(-1)
```

### Step 7: Assign fwd_meg = pick_channels_forward(...)

```python
fwd_meg = pick_channels_forward(fwd_op, bad_info['ch_names'][:306])
```

### Step 8: Assign inv_meg = make_inverse_operator(...)

```python
inv_meg = make_inverse_operator(bad_info, fwd_meg, noise_cov)
```

### Step 9: Assign raw = mne.io.RawArray(...)

```python
raw = mne.io.RawArray(data, bad_info)
```

### Step 10: Assign epochs = make_fixed_length_epochs.load_data(...)

```python
epochs = make_fixed_length_epochs(raw, duration=tmax).load_data()
```

**Verification:**
```python
assert len(epochs) == 1
```

### Step 11: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 12: Assign evoked_cust = epochs.average.set_eeg_reference(...)

```python
evoked_cust = epochs.average().set_eeg_reference()
```

**Verification:**
```python
assert evoked_cust.info['custom_ref_applied']
```

### Step 13: Assign unknown = list(...)

```python
bad_info['projs'] = list()
```

### Step 14: Call make_inverse_operator()

```python
make_inverse_operator(bad_info, fwd_op, noise_cov, depth=-0.1)
```

### Step 15: Assign inv = make_inverse_operator(...)

```python
inv = make_inverse_operator(bad_info, fwd_op, noise_cov)
```

### Step 16: Call func()

```python
func(inst, inv_meg, 1.0 / 9.0)
```

### Step 17: Call func()

```python
func(inst, inv, 1.0 / 9.0)
```


## Complete Example

```python
# Setup
# Fixtures: evoked, noise_cov

# Workflow
'Test MNE inverse warning without average EEG projection.'
bad_info = evoked.info
data = evoked.data
tmax = evoked.tmax
del evoked
with bad_info._unlock():
    bad_info['projs'] = list()
assert bad_info['bads'] == ['MEG 2443', 'EEG 053']
fwd_op = convert_forward_solution(read_forward_solution(fname_fwd), surf_ori=True, copy=False)
with pytest.raises(ValueError, match='greater than or'):
    make_inverse_operator(bad_info, fwd_op, noise_cov, depth=-0.1)
noise_cov['projs'].pop(-1)
with pytest.warns(RuntimeWarning, match='reference'):
    inv = make_inverse_operator(bad_info, fwd_op, noise_cov)
fwd_meg = pick_channels_forward(fwd_op, bad_info['ch_names'][:306])
inv_meg = make_inverse_operator(bad_info, fwd_meg, noise_cov)
raw = mne.io.RawArray(data, bad_info)
epochs = make_fixed_length_epochs(raw, duration=tmax).load_data()
assert len(epochs) == 1
evoked = epochs.average()
evoked_cust = epochs.average().set_eeg_reference()
assert evoked_cust.info['custom_ref_applied']
assert 'eeg' in raw
assert 'meg' in raw
for func, inst in ((apply_inverse_raw, raw), (apply_inverse_epochs, epochs), (apply_inverse, evoked), (apply_inverse, evoked_cust)):
    with pytest.raises(ValueError, match='reference'):
        func(inst, inv, 1.0 / 9.0)
    func(inst, inv_meg, 1.0 / 9.0)
```

## Next Steps


---

*Source: test_inverse.py:253 | Complexity: Advanced | Last updated: 2026-05-18*