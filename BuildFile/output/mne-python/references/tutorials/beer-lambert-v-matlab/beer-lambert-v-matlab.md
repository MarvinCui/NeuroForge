# How To: Beer Lambert V Matlab

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Compare MNE results to MATLAB toolbox.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.preprocessing.nirs._beer_lambert_law`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Compare MNE results to MATLAB toolbox.'

```python
'Compare MNE results to MATLAB toolbox.'
```

**Verification:**
```python
assert mean_error < 0.1
```

### Step 2: Assign pymatreader = pytest.importorskip(...)

```python
pymatreader = pytest.importorskip('pymatreader')
```

**Verification:**
```python
assert raw.info['ch_names'][idx] == matlab_name
```

### Step 3: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname_nirx_15_0)
```

### Step 4: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 5: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw, ppf=(0.121, 0.121))
```

### Step 6: Assign matlab_fname = value

```python
matlab_fname = testing_path / 'NIRx' / 'nirscout' / 'validation' / 'nirx_15_0_recording_bl.mat'
```

### Step 7: Assign matlab_data = pymatreader.read_mat(...)

```python
matlab_data = pymatreader.read_mat(matlab_fname)
```

### Step 8: Assign mean_error = np.mean(...)

```python
mean_error = np.mean(matlab_data['data'][:, idx] - raw._data[idx])
```

**Verification:**
```python
assert mean_error < 0.1
```

### Step 9: Assign matlab_name = value

```python
matlab_name = 'S' + str(int(matlab_data['sources'][idx])) + '_D' + str(int(matlab_data['detectors'][idx])) + ' ' + matlab_data['type'][idx]
```

**Verification:**
```python
assert raw.info['ch_names'][idx] == matlab_name
```


## Complete Example

```python
# Workflow
'Compare MNE results to MATLAB toolbox.'
pymatreader = pytest.importorskip('pymatreader')
raw = read_raw_nirx(fname_nirx_15_0)
raw = optical_density(raw)
raw = beer_lambert_law(raw, ppf=(0.121, 0.121))
raw._data *= 1000000.0
matlab_fname = testing_path / 'NIRx' / 'nirscout' / 'validation' / 'nirx_15_0_recording_bl.mat'
matlab_data = pymatreader.read_mat(matlab_fname)
for idx in range(raw.get_data().shape[0]):
    mean_error = np.mean(matlab_data['data'][:, idx] - raw._data[idx])
    assert mean_error < 0.1
    matlab_name = 'S' + str(int(matlab_data['sources'][idx])) + '_D' + str(int(matlab_data['detectors'][idx])) + ' ' + matlab_data['type'][idx]
    assert raw.info['ch_names'][idx] == matlab_name
```

## Next Steps


---

*Source: test_beer_lambert_law.py:95 | Complexity: Advanced | Last updated: 2026-05-18*