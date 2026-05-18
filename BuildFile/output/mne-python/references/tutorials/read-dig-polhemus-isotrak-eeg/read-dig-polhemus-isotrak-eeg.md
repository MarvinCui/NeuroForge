# How To: Read Dig Polhemus Isotrak Eeg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading Polhemus IsoTrak EEG positions.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `contextlib`
- `functools`
- `itertools`
- `pathlib`
- `string`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.montage`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.channels.montage`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.io.kit`
- `mne.preprocessing`
- `mne.transforms`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz._3d`

**Setup Required:**
```python
# Fixtures: isotrak_eeg
```

## Step-by-Step Guide

### Step 1: 'Test reading Polhemus IsoTrak EEG positions.'

```python
'Test reading Polhemus IsoTrak EEG positions.'
```

**Verification:**
```python
assert repr(montage) == '<DigMontage | 0 extras (headshape), 0 HPIs, 3 fiducials, 5 channels>'
```

### Step 2: Assign N_CHANNELS = 5

```python
N_CHANNELS = 5
```

**Verification:**
```python
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
```

### Step 3: Assign _SEED = 42

```python
_SEED = 42
```

**Verification:**
```python
assert_array_equal(val, EXPECTED_FID_IN_POLHEMUS[kk])
```

### Step 4: Assign EXPECTED_FID_IN_POLHEMUS = value

```python
EXPECTED_FID_IN_POLHEMUS = {'nasion': np.array([0.11056, -5.421e-19, 0]), 'lpa': np.array([-0.00021075, 0.080793, -7.5894e-19]), 'rpa': np.array([0.00021075, -0.080793, -2.8731e-18])}
```

**Verification:**
```python
assert_array_equal(dig_point['r'], EXPECTED_CH_POS[kk])
```

### Step 5: Assign ch_names = value

```python
ch_names = [f'eeg {ii:01d}' for ii in range(N_CHANNELS)]
```

**Verification:**
```python
assert dig_point['coord_frame'] == FIFF.FIFFV_COORD_UNKNOWN
```

### Step 6: Assign EXPECTED_CH_POS = dict(...)

```python
EXPECTED_CH_POS = dict(zip(ch_names, np.random.RandomState(_SEED).randn(N_CHANNELS, 3)))
```

### Step 7: Assign montage = read_dig_polhemus_isotrak(...)

```python
montage = read_dig_polhemus_isotrak(fname=isotrak_eeg, ch_names=ch_names)
```

**Verification:**
```python
assert repr(montage) == '<DigMontage | 0 extras (headshape), 0 HPIs, 3 fiducials, 5 channels>'
```

### Step 8: Assign unknown = _get_fid_coords(...)

```python
fiducials, fid_coordframe = _get_fid_coords(montage.dig)
```

**Verification:**
```python
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(val, EXPECTED_FID_IN_POLHEMUS[kk])
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(dig_point['r'], EXPECTED_CH_POS[kk])
```

**Verification:**
```python
assert dig_point['coord_frame'] == FIFF.FIFFV_COORD_UNKNOWN
```


## Complete Example

```python
# Setup
# Fixtures: isotrak_eeg

# Workflow
'Test reading Polhemus IsoTrak EEG positions.'
N_CHANNELS = 5
_SEED = 42
EXPECTED_FID_IN_POLHEMUS = {'nasion': np.array([0.11056, -5.421e-19, 0]), 'lpa': np.array([-0.00021075, 0.080793, -7.5894e-19]), 'rpa': np.array([0.00021075, -0.080793, -2.8731e-18])}
ch_names = [f'eeg {ii:01d}' for ii in range(N_CHANNELS)]
EXPECTED_CH_POS = dict(zip(ch_names, np.random.RandomState(_SEED).randn(N_CHANNELS, 3)))
montage = read_dig_polhemus_isotrak(fname=isotrak_eeg, ch_names=ch_names)
assert repr(montage) == '<DigMontage | 0 extras (headshape), 0 HPIs, 3 fiducials, 5 channels>'
fiducials, fid_coordframe = _get_fid_coords(montage.dig)
assert fid_coordframe == FIFF.FIFFV_COORD_UNKNOWN
for kk, val in fiducials.items():
    assert_array_equal(val, EXPECTED_FID_IN_POLHEMUS[kk])
for kk, dig_point in zip(montage.ch_names, _get_dig_eeg(montage.dig)):
    assert_array_equal(dig_point['r'], EXPECTED_CH_POS[kk])
    assert dig_point['coord_frame'] == FIFF.FIFFV_COORD_UNKNOWN
```

## Next Steps


---

*Source: test_montage.py:824 | Complexity: Advanced | Last updated: 2026-05-18*