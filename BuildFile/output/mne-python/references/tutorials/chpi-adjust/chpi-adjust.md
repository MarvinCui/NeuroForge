# How To: Chpi Adjust

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test cHPI logging and adjustment.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.interpolate`
- `scipy.spatial.distance`
- `mne`
- `mne._fiff.constants`
- `mne.chpi`
- `mne.datasets`
- `mne.forward._compute_forward`
- `mne.io`
- `mne.simulation`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz`
- `scipy.signal`


## Step-by-Step Guide

### Step 1: 'Test cHPI logging and adjustment.'

```python
'Test cHPI logging and adjustment.'
```

**Verification:**
```python
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
```

**Verification:**
```python
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
```

### Step 3: Assign msg = value

```python
msg = ['HPIFIT: 5 coils digitized in order 5 1 4 3 2', 'HPIFIT: 3 coils accepted: 1 2 4', 'HPI coil moments (3, 5):', '2.08542e-15 -1.52486e-15 -1.53484e-15', '2.14516e-15 2.09608e-15 7.30303e-16', '-3.2318e-16 -4.25666e-16 2.69997e-15', '5.21717e-16 1.28406e-15 1.95335e-15', '1.21199e-15 -1.25801e-19 1.18321e-15', 'HPIFIT errors:  0.3, 0.3, 5.3, 0.4, 3.2 mm.', 'HPI consistency of isotrak and hpifit is OK.', 'HP fitting limits: err = 5.0 mm, gval = 0.980.', 'Using 5 HPI coils: 83 143 203 263 323 Hz']
```

### Step 4: Assign log = log.getvalue.splitlines(...)

```python
log = log.getvalue().splitlines()
```

**Verification:**
```python
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
```

### Step 5: Assign msg = value

```python
msg = msg[:8] + ['HPIFIT errors:  0.3, 0.3, 5.3, 999.7, 3.2 mm.', 'Note: HPI coil 3 isotrak is adjusted by 5.3 mm!', 'Note: HPI coil 5 isotrak is adjusted by 3.2 mm!'] + msg[-2:]
```

### Step 6: Assign log = log.getvalue.splitlines(...)

```python
log = log.getvalue().splitlines()
```

**Verification:**
```python
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
```

### Step 7: Call _get_hpi_initial_fit()

```python
_get_hpi_initial_fit(raw.info, adjust=True, verbose='debug')
```

### Step 8: Call get_chpi_info()

```python
get_chpi_info(raw.info, on_missing='raise', verbose='debug')
```

### Step 9: Call _get_hpi_initial_fit()

```python
_get_hpi_initial_fit(raw.info, adjust=True, verbose='debug')
```

### Step 10: Call get_chpi_info()

```python
get_chpi_info(raw.info, on_missing='raise', verbose='debug')
```


## Complete Example

```python
# Workflow
'Test cHPI logging and adjustment.'
raw = read_raw_fif(chpi_fif_fname, allow_maxshield='yes')
with catch_logging() as log:
    _get_hpi_initial_fit(raw.info, adjust=True, verbose='debug')
    get_chpi_info(raw.info, on_missing='raise', verbose='debug')
msg = ['HPIFIT: 5 coils digitized in order 5 1 4 3 2', 'HPIFIT: 3 coils accepted: 1 2 4', 'HPI coil moments (3, 5):', '2.08542e-15 -1.52486e-15 -1.53484e-15', '2.14516e-15 2.09608e-15 7.30303e-16', '-3.2318e-16 -4.25666e-16 2.69997e-15', '5.21717e-16 1.28406e-15 1.95335e-15', '1.21199e-15 -1.25801e-19 1.18321e-15', 'HPIFIT errors:  0.3, 0.3, 5.3, 0.4, 3.2 mm.', 'HPI consistency of isotrak and hpifit is OK.', 'HP fitting limits: err = 5.0 mm, gval = 0.980.', 'Using 5 HPI coils: 83 143 203 263 323 Hz']
log = log.getvalue().splitlines()
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
raw.info['dig'][5]['r'][2] += 1.0
msg = msg[:8] + ['HPIFIT errors:  0.3, 0.3, 5.3, 999.7, 3.2 mm.', 'Note: HPI coil 3 isotrak is adjusted by 5.3 mm!', 'Note: HPI coil 5 isotrak is adjusted by 3.2 mm!'] + msg[-2:]
with catch_logging() as log:
    _get_hpi_initial_fit(raw.info, adjust=True, verbose='debug')
    get_chpi_info(raw.info, on_missing='raise', verbose='debug')
log = log.getvalue().splitlines()
assert set(log) == set(msg), '\n' + '\n'.join(set(msg) - set(log))
```

## Next Steps


---

*Source: test_chpi.py:98 | Complexity: Advanced | Last updated: 2026-05-18*