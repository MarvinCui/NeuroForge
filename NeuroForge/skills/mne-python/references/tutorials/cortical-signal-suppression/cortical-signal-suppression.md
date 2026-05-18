# How To: Cortical Signal Suppression

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that CSS is dampening the cortical signal and has right shape.

## Prerequisites

**Required Modules:**
- `numpy`
- `mne`
- `mne.datasets`
- `mne.preprocessing._css`


## Step-by-Step Guide

### Step 1: 'Test that CSS is dampening the cortical signal and has right shape.'

```python
'Test that CSS is dampening the cortical signal and has right shape.'
```

**Verification:**
```python
assert ave_f.data.shape == ave.data.shape
```

### Step 2: Assign ave = value

```python
ave = read_evokeds(fname_evoked)[0]
```

**Verification:**
```python
assert rel_SNR_gain > 3, mag_picks
```

### Step 3: Assign eeg_ind = pick_types(...)

```python
eeg_ind = pick_types(ave.info, eeg=True)
```

### Step 4: Assign mag_ind = pick_types(...)

```python
mag_ind = pick_types(ave.info, meg='mag')
```

### Step 5: Assign grad_ind = pick_types(...)

```python
grad_ind = pick_types(ave.info, meg='grad')
```

### Step 6: Assign unknown = value

```python
ave.data[mag_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[mag_ind][0, :]))
```

### Step 7: Assign unknown = value

```python
ave.data[mag_ind][1, :] = np.sin(2 * np.pi * 239 * ave.times) * np.mean(np.abs(ave.data[mag_ind][1, :]))
```

### Step 8: Assign unknown = value

```python
ave.data[grad_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[grad_ind][0, :]))
```

### Step 9: Assign unknown = value

```python
ave.data[eeg_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[eeg_ind][0, :]))
```

### Step 10: Assign unknown = value

```python
ave.data[eeg_ind][1, :] = np.sin(2 * np.pi * 239 * ave.times) * np.mean(np.abs(ave.data[eeg_ind][1, :]))
```

### Step 11: Assign ave_f = cortical_signal_suppression(...)

```python
ave_f = cortical_signal_suppression(ave, mag_picks=mag_picks)
```

**Verification:**
```python
assert ave_f.data.shape == ave.data.shape
```

### Step 12: Assign cort_power = np.linalg.norm(...)

```python
cort_power = np.linalg.norm(ave.data[ind][0, :])
```

### Step 13: Assign deep_power = np.linalg.norm(...)

```python
deep_power = np.linalg.norm(ave.data[ind][1, :])
```

### Step 14: Assign cort_power_f = np.linalg.norm(...)

```python
cort_power_f = np.linalg.norm(ave_f.data[ind][0, :])
```

### Step 15: Assign deep_power_f = np.linalg.norm(...)

```python
deep_power_f = np.linalg.norm(ave_f.data[ind][1, :])
```

### Step 16: Assign rel_SNR_gain = value

```python
rel_SNR_gain = deep_power_f / deep_power / (cort_power_f / cort_power)
```

**Verification:**
```python
assert rel_SNR_gain > 3, mag_picks
```


## Complete Example

```python
# Workflow
'Test that CSS is dampening the cortical signal and has right shape.'
ave = read_evokeds(fname_evoked)[0]
eeg_ind = pick_types(ave.info, eeg=True)
mag_ind = pick_types(ave.info, meg='mag')
grad_ind = pick_types(ave.info, meg='grad')
ave.data[mag_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[mag_ind][0, :]))
ave.data[mag_ind][1, :] = np.sin(2 * np.pi * 239 * ave.times) * np.mean(np.abs(ave.data[mag_ind][1, :]))
ave.data[grad_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[grad_ind][0, :]))
ave.data[eeg_ind][0, :] = np.sin(2 * np.pi * 40 * ave.times) * np.mean(np.abs(ave.data[eeg_ind][0, :]))
ave.data[eeg_ind][1, :] = np.sin(2 * np.pi * 239 * ave.times) * np.mean(np.abs(ave.data[eeg_ind][1, :]))
for mag_picks, ind in ((None, eeg_ind), ('eeg', mag_ind)):
    ave_f = cortical_signal_suppression(ave, mag_picks=mag_picks)
    assert ave_f.data.shape == ave.data.shape
    cort_power = np.linalg.norm(ave.data[ind][0, :])
    deep_power = np.linalg.norm(ave.data[ind][1, :])
    cort_power_f = np.linalg.norm(ave_f.data[ind][0, :])
    deep_power_f = np.linalg.norm(ave_f.data[ind][1, :])
    rel_SNR_gain = deep_power_f / deep_power / (cort_power_f / cort_power)
    assert rel_SNR_gain > 3, mag_picks
```

## Next Steps


---

*Source: test_css.py:16 | Complexity: Advanced | Last updated: 2026-05-18*