# How To: Mne Python Vs Eeglab

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test eeglab vs mne_python infomax code.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy.linalg`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.infomax_`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test eeglab vs mne_python infomax code.'

```python
'Test eeglab vs mne_python infomax code.'
```

**Verification:**
```python
assert_almost_equal(maximum_difference, 1e-12, decimal=10)
```

### Step 2: Assign random_state = 42

```python
random_state = 42
```

### Step 3: Assign methods = value

```python
methods = ['infomax', 'extended_infomax']
```

### Step 4: Assign ch_types = value

```python
ch_types = ['eeg', 'mag']
```

### Step 5: Assign Y = generate_data_for_comparing_against_eeglab_infomax(...)

```python
Y = generate_data_for_comparing_against_eeglab_infomax(ch_type, random_state)
```

### Step 6: Assign unknown = value

```python
N, T = Y.shape
```

### Step 7: Assign eeglab_results_file = value

```python
eeglab_results_file = f"eeglab_{method}_results_{dict(eeg='eeg', mag='meg')[ch_type]}_data.mat"
```

### Step 8: Assign l_rate_eeglab = value

```python
l_rate_eeglab = 0.00065 / np.log(N)
```

### Step 9: Assign block_eeglab = int(...)

```python
block_eeglab = int(np.ceil(np.min([5 * np.log(T), 0.3 * T])))
```

### Step 10: Assign blowup_eeglab = 1000000000.0

```python
blowup_eeglab = 1000000000.0
```

### Step 11: Assign blowup_fac_eeglab = 0.8

```python
blowup_fac_eeglab = 0.8
```

### Step 12: Assign max_iter_eeglab = 512

```python
max_iter_eeglab = 512
```

### Step 13: Assign w_change_eeglab = value

```python
w_change_eeglab = 1e-07 if N > 32 else 1e-06
```

### Step 14: Assign unmixing = infomax(...)

```python
unmixing = infomax(Y.T, extended=use_extended, random_state=random_state, max_iter=max_iter_eeglab, l_rate=l_rate_eeglab, block=block_eeglab, w_change=w_change_eeglab, blowup=blowup_eeglab, blowup_fac=blowup_fac_eeglab, n_small_angle=None, anneal_step=anneal_step_eeglab)
```

### Step 15: Assign sources = np.dot(...)

```python
sources = np.dot(unmixing, Y)
```

### Step 16: Assign mixing = pinv(...)

```python
mixing = pinv(unmixing)
```

### Step 17: Assign mvar = value

```python
mvar = np.sum(mixing ** 2, axis=0) * np.sum(sources ** 2, axis=1) / (N * T - 1)
```

### Step 18: Assign windex = value

```python
windex = np.argsort(mvar)[::-1]
```

### Step 19: Assign unmixing_ordered = value

```python
unmixing_ordered = unmixing[windex, :]
```

### Step 20: Assign eeglab_data = sio.loadmat(...)

```python
eeglab_data = sio.loadmat(base_dir / eeglab_results_file)
```

### Step 21: Assign unmixing_eeglab = value

```python
unmixing_eeglab = eeglab_data['unmixing_eeglab']
```

### Step 22: Assign maximum_difference = np.max(...)

```python
maximum_difference = np.max(np.abs(unmixing_ordered - unmixing_eeglab))
```

### Step 23: Call assert_almost_equal()

```python
assert_almost_equal(maximum_difference, 1e-12, decimal=10)
```

### Step 24: Assign anneal_step_eeglab = 0.9

```python
anneal_step_eeglab = 0.9
```

### Step 25: Assign use_extended = False

```python
use_extended = False
```

### Step 26: Assign anneal_step_eeglab = 0.98

```python
anneal_step_eeglab = 0.98
```

### Step 27: Assign use_extended = True

```python
use_extended = True
```


## Complete Example

```python
# Workflow
'Test eeglab vs mne_python infomax code.'
random_state = 42
methods = ['infomax', 'extended_infomax']
ch_types = ['eeg', 'mag']
for ch_type in ch_types:
    Y = generate_data_for_comparing_against_eeglab_infomax(ch_type, random_state)
    N, T = Y.shape
    for method in methods:
        eeglab_results_file = f"eeglab_{method}_results_{dict(eeg='eeg', mag='meg')[ch_type]}_data.mat"
        l_rate_eeglab = 0.00065 / np.log(N)
        block_eeglab = int(np.ceil(np.min([5 * np.log(T), 0.3 * T])))
        blowup_eeglab = 1000000000.0
        blowup_fac_eeglab = 0.8
        max_iter_eeglab = 512
        if method == 'infomax':
            anneal_step_eeglab = 0.9
            use_extended = False
        elif method == 'extended_infomax':
            anneal_step_eeglab = 0.98
            use_extended = True
        w_change_eeglab = 1e-07 if N > 32 else 1e-06
        unmixing = infomax(Y.T, extended=use_extended, random_state=random_state, max_iter=max_iter_eeglab, l_rate=l_rate_eeglab, block=block_eeglab, w_change=w_change_eeglab, blowup=blowup_eeglab, blowup_fac=blowup_fac_eeglab, n_small_angle=None, anneal_step=anneal_step_eeglab)
        sources = np.dot(unmixing, Y)
        mixing = pinv(unmixing)
        mvar = np.sum(mixing ** 2, axis=0) * np.sum(sources ** 2, axis=1) / (N * T - 1)
        windex = np.argsort(mvar)[::-1]
        unmixing_ordered = unmixing[windex, :]
        eeglab_data = sio.loadmat(base_dir / eeglab_results_file)
        unmixing_eeglab = eeglab_data['unmixing_eeglab']
        maximum_difference = np.max(np.abs(unmixing_ordered - unmixing_eeglab))
        assert_almost_equal(maximum_difference, 1e-12, decimal=10)
```

## Next Steps


---

*Source: test_eeglab_infomax.py:72 | Complexity: Advanced | Last updated: 2026-05-18*