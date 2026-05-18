# How To: Check Info Inv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test checks for common channels across fwd model and cov matrices.

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.utils`
- `types`


## Step-by-Step Guide

### Step 1: 'Test checks for common channels across fwd model and cov matrices.'

```python
'Test checks for common channels across fwd model and cov matrices.'
```

**Verification:**
```python
assert epochs.info['ch_names'] == data_cov.ch_names
```

### Step 2: Assign unknown = _get_data(...)

```python
epochs, data_cov, noise_cov, forward = _get_data()
```

**Verification:**
```python
assert epochs.info['ch_names'] == noise_cov.ch_names
```

### Step 3: Assign info_bads = epochs.info.copy(...)

```python
info_bads = epochs.info.copy()
```

**Verification:**
```python
assert [1, 2] not in picks
```

### Step 4: Assign unknown = value

```python
info_bads['bads'] = info_bads['ch_names'][1:3]
```

**Verification:**
```python
assert 0 not in picks
```

### Step 5: Assign picks = _check_info_inv(...)

```python
picks = _check_info_inv(info_bads, forward, noise_cov=noise_cov)
```

**Verification:**
```python
assert 1 not in picks
```

### Step 6: Assign data_cov_bads = data_cov.copy(...)

```python
data_cov_bads = data_cov.copy()
```

**Verification:**
```python
assert 0 not in picks
```

### Step 7: Assign unknown = value

```python
data_cov_bads['bads'] = [data_cov_bads.ch_names[0]]
```

**Verification:**
```python
assert list(range(7, 10)) == picks
```

### Step 8: Assign picks = _check_info_inv(...)

```python
picks = _check_info_inv(epochs.info, forward, data_cov=data_cov_bads)
```

**Verification:**
```python
assert 'Excluding 7 channel(s) missing' in log
```

### Step 9: Assign noise_cov_bads = noise_cov.copy(...)

```python
noise_cov_bads = noise_cov.copy()
```

### Step 10: Assign unknown = value

```python
noise_cov_bads['bads'] = [noise_cov_bads.ch_names[1]]
```

### Step 11: Assign picks = _check_info_inv(...)

```python
picks = _check_info_inv(epochs.info, forward, noise_cov=noise_cov_bads)
```

**Verification:**
```python
assert 1 not in picks
```

### Step 12: Assign info_ref = epochs.info.copy(...)

```python
info_ref = epochs.info.copy()
```

### Step 13: Assign unknown = 301

```python
info_ref['chs'][0]['kind'] = 301
```

### Step 14: Assign picks = _check_info_inv(...)

```python
picks = _check_info_inv(info_ref, forward, noise_cov=noise_cov)
```

**Verification:**
```python
assert 0 not in picks
```

### Step 15: Call epochs.pick()

```python
epochs.pick([epochs.ch_names[ii] for ii in range(10)])
```

### Step 16: Assign data_cov = pick_channels_cov(...)

```python
data_cov = pick_channels_cov(data_cov, include=[data_cov.ch_names[ii] for ii in range(5, 20)])
```

### Step 17: Assign noise_cov = pick_channels_cov(...)

```python
noise_cov = pick_channels_cov(noise_cov, include=[noise_cov.ch_names[ii] for ii in range(7, 12)])
```

### Step 18: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'Excluding 7 channel(s) missing' in log
```

### Step 19: Assign picks = _check_info_inv(...)

```python
picks = _check_info_inv(epochs.info, forward, noise_cov=noise_cov, data_cov=data_cov, verbose=True)
```

**Verification:**
```python
assert list(range(7, 10)) == picks
```


## Complete Example

```python
# Workflow
'Test checks for common channels across fwd model and cov matrices.'
epochs, data_cov, noise_cov, forward = _get_data()
assert epochs.info['ch_names'] == data_cov.ch_names
assert epochs.info['ch_names'] == noise_cov.ch_names
info_bads = epochs.info.copy()
info_bads['bads'] = info_bads['ch_names'][1:3]
picks = _check_info_inv(info_bads, forward, noise_cov=noise_cov)
assert [1, 2] not in picks
data_cov_bads = data_cov.copy()
data_cov_bads['bads'] = [data_cov_bads.ch_names[0]]
picks = _check_info_inv(epochs.info, forward, data_cov=data_cov_bads)
assert 0 not in picks
noise_cov_bads = noise_cov.copy()
noise_cov_bads['bads'] = [noise_cov_bads.ch_names[1]]
picks = _check_info_inv(epochs.info, forward, noise_cov=noise_cov_bads)
assert 1 not in picks
info_ref = epochs.info.copy()
info_ref['chs'][0]['kind'] = 301
picks = _check_info_inv(info_ref, forward, noise_cov=noise_cov)
assert 0 not in picks
epochs.pick([epochs.ch_names[ii] for ii in range(10)])
data_cov = pick_channels_cov(data_cov, include=[data_cov.ch_names[ii] for ii in range(5, 20)])
noise_cov = pick_channels_cov(noise_cov, include=[noise_cov.ch_names[ii] for ii in range(7, 12)])
with catch_logging() as log:
    picks = _check_info_inv(epochs.info, forward, noise_cov=noise_cov, data_cov=data_cov, verbose=True)
    assert list(range(7, 10)) == picks
log = log.getvalue()
assert 'Excluding 7 channel(s) missing' in log
```

## Next Steps


---

*Source: test_check.py:132 | Complexity: Advanced | Last updated: 2026-05-18*