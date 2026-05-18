# How To: Stim Eog Misc Chs In Nsx

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test stim/misc/eog channel assignments.

## Prerequisites

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.nsx.nsx`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test stim/misc/eog channel assignments.'

```python
'Test stim/misc/eog channel assignments.'
```

**Verification:**
```python
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
```

### Step 2: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel='elec127', eog=['elec126'])
```

**Verification:**
```python
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
```

### Step 3: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel=['elec127'], eog=['elec126'])
```

**Verification:**
```python
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
```

### Step 4: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel=127, eog=['elec126'])
```

**Verification:**
```python
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
```

### Step 5: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel=[127], eog=['elec126'])
```

**Verification:**
```python
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
```

### Step 6: Assign stims = value

```python
stims = [ch_info['kind'] == FIFF.FIFFV_STIM_CH for ch_info in raw.info['chs']]
```

**Verification:**
```python
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
```

### Step 7: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel='elec127', misc=['elec126', 'elec1'])
```

**Verification:**
```python
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
```

### Step 8: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel=['elec128', 129], eog=['elec126'])
```

**Verification:**
```python
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
```

### Step 9: Assign raw = read_raw_nsx(...)

```python
raw = read_raw_nsx(nsx_22_fname, stim_channel=('elec128',), eog=['elec126'])
```

**Verification:**
```python
assert np.any(stims)
```


## Complete Example

```python
# Workflow
'Test stim/misc/eog channel assignments.'
raw = read_raw_nsx(nsx_22_fname, stim_channel='elec127', eog=['elec126'])
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
raw = read_raw_nsx(nsx_22_fname, stim_channel=['elec127'], eog=['elec126'])
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
raw = read_raw_nsx(nsx_22_fname, stim_channel=127, eog=['elec126'])
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
raw = read_raw_nsx(nsx_22_fname, stim_channel=[127], eog=['elec126'])
assert raw.info['chs'][127]['kind'] == FIFF.FIFFV_STIM_CH
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
stims = [ch_info['kind'] == FIFF.FIFFV_STIM_CH for ch_info in raw.info['chs']]
assert np.any(stims)
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_EOG_CH
with pytest.raises(ValueError, match='Invalid stim_channel'):
    raw = read_raw_nsx(nsx_22_fname, stim_channel=['elec128', 129], eog=['elec126'])
with pytest.raises(ValueError, match='Invalid stim_channel'):
    raw = read_raw_nsx(nsx_22_fname, stim_channel=('elec128',), eog=['elec126'])
raw = read_raw_nsx(nsx_22_fname, stim_channel='elec127', misc=['elec126', 'elec1'])
assert raw.info['chs'][126]['kind'] == FIFF.FIFFV_MISC_CH
assert raw.info['chs'][1]['kind'] == FIFF.FIFFV_MISC_CH
```

## Next Steps


---

*Source: test_nsx.py:198 | Complexity: Advanced | Last updated: 2026-05-18*