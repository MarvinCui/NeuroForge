# How To: Interpolate Meg Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interpolation of MEG channels from CTF system.

## Prerequisites

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.channels.channels`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.proj`
- `mne.channels`
- `mne.channels.interpolation`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing.nirs`
- `mne.utils`
- `mne.channels.interpolation`


## Step-by-Step Guide

### Step 1: 'Test interpolation of MEG channels from CTF system.'

```python
'Test interpolation of MEG channels from CTF system.'
```

**Verification:**
```python
assert R['no_refmeg'] > R['with_refmeg'] + tol
```

### Step 2: Assign thresh = 0.85

```python
thresh = 0.85
```

**Verification:**
```python
assert R['no_refmeg'] > thresh
```

### Step 3: Assign tol = 0.05

```python
tol = 0.05
```

### Step 4: Assign bad = 'MLC22-2622'

```python
bad = 'MLC22-2622'
```

### Step 5: Assign raw = read_raw_fif.crop.load_data(...)

```python
raw = read_raw_fif(raw_fname_ctf).crop(0, 1.0).load_data()
```

### Step 6: Call raw.apply_gradient_compensation()

```python
raw.apply_gradient_compensation(3)
```

### Step 7: Assign unknown = value

```python
raw.info['bads'] = [bad]
```

### Step 8: Assign pick_bad = pick_channels(...)

```python
pick_bad = pick_channels(raw.info['ch_names'], raw.info['bads'])
```

### Step 9: Assign data_orig = value

```python
data_orig = raw[pick_bad, :][0]
```

### Step 10: Assign data_interp_refmeg = value

```python
data_interp_refmeg = _this_interpol(raw, ref_meg=True)[pick_bad, :][0]
```

### Step 11: Assign data_interp_no_refmeg = value

```python
data_interp_no_refmeg = _this_interpol(raw, ref_meg=False)[pick_bad, :][0]
```

### Step 12: Assign R = dict(...)

```python
R = dict()
```

### Step 13: Assign unknown = value

```python
R['no_refmeg'] = np.corrcoef(data_orig, data_interp_no_refmeg)[0, 1]
```

### Step 14: Assign unknown = value

```python
R['with_refmeg'] = np.corrcoef(data_orig, data_interp_refmeg)[0, 1]
```

### Step 15: Call print()

```python
print('Corrcoef of interpolated with original channel: ', R)
```

**Verification:**
```python
assert R['no_refmeg'] > R['with_refmeg'] + tol
```


## Complete Example

```python
# Workflow
'Test interpolation of MEG channels from CTF system.'
thresh = 0.85
tol = 0.05
bad = 'MLC22-2622'
raw = read_raw_fif(raw_fname_ctf).crop(0, 1.0).load_data()
raw.apply_gradient_compensation(3)
raw.info['bads'] = [bad]
pick_bad = pick_channels(raw.info['ch_names'], raw.info['bads'])
data_orig = raw[pick_bad, :][0]
data_interp_refmeg = _this_interpol(raw, ref_meg=True)[pick_bad, :][0]
data_interp_no_refmeg = _this_interpol(raw, ref_meg=False)[pick_bad, :][0]
R = dict()
R['no_refmeg'] = np.corrcoef(data_orig, data_interp_no_refmeg)[0, 1]
R['with_refmeg'] = np.corrcoef(data_orig, data_interp_refmeg)[0, 1]
print('Corrcoef of interpolated with original channel: ', R)
assert R['no_refmeg'] > R['with_refmeg'] + tol
assert R['no_refmeg'] > thresh
```

## Next Steps


---

*Source: test_interpolation.py:273 | Complexity: Advanced | Last updated: 2026-05-18*