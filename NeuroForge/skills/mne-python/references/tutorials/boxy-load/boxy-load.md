# How To: Boxy Load

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading BOXY files.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test reading BOXY files.'

```python
'Test reading BOXY files.'
```

**Verification:**
```python
assert raw.info['sfreq'] == 62.5
```

### Step 2: Assign raw = read_raw_boxy(...)

```python
raw = read_raw_boxy(boxy_0_40, verbose=True)
```

**Verification:**
```python
assert mne_dc.info['ch_names'][:10] == [i_chan + ' ' + 'DC' for i_chan in first_chans]
```

### Step 3: Call _assert_ppod()

```python
_assert_ppod(raw, p_pod_0_40)
```

**Verification:**
```python
assert mne_ac.info['ch_names'][:10] == [i_chan + ' ' + 'AC' for i_chan in first_chans]
```

### Step 4: Assign mne_ph = raw.copy.pick(...)

```python
mne_ph = raw.copy().pick(picks='fnirs_fd_phase')
```

**Verification:**
```python
assert mne_ph.info['ch_names'][:10] == [i_chan + ' ' + 'Ph' for i_chan in first_chans]
```

### Step 5: Assign mne_dc = raw.copy.pick(...)

```python
mne_dc = raw.copy().pick(picks='fnirs_cw_amplitude')
```

**Verification:**
```python
assert mne_dc.info['ch_names'][70:] == [i_chan + ' ' + 'DC' for i_chan in last_chans]
```

### Step 6: Assign mne_ac = raw.copy.pick(...)

```python
mne_ac = raw.copy().pick(picks='fnirs_fd_ac_amplitude')
```

**Verification:**
```python
assert mne_ac.info['ch_names'][70:] == [i_chan + ' ' + 'AC' for i_chan in last_chans]
```

### Step 7: Assign first_chans = value

```python
first_chans = ['S1_D1', 'S2_D1', 'S3_D1', 'S4_D1', 'S5_D1', 'S6_D1', 'S7_D1', 'S8_D1', 'S9_D1', 'S10_D1']
```

**Verification:**
```python
assert mne_ph.info['ch_names'][70:] == [i_chan + ' ' + 'Ph' for i_chan in last_chans]
```

### Step 8: Assign last_chans = value

```python
last_chans = ['S1_D8', 'S2_D8', 'S3_D8', 'S4_D8', 'S5_D8', 'S6_D8', 'S7_D8', 'S8_D8', 'S9_D8', 'S10_D8']
```

**Verification:**
```python
assert len(raw.annotations) == 0
```


## Complete Example

```python
# Workflow
'Test reading BOXY files.'
raw = read_raw_boxy(boxy_0_40, verbose=True)
assert raw.info['sfreq'] == 62.5
_assert_ppod(raw, p_pod_0_40)
mne_ph = raw.copy().pick(picks='fnirs_fd_phase')
mne_dc = raw.copy().pick(picks='fnirs_cw_amplitude')
mne_ac = raw.copy().pick(picks='fnirs_fd_ac_amplitude')
first_chans = ['S1_D1', 'S2_D1', 'S3_D1', 'S4_D1', 'S5_D1', 'S6_D1', 'S7_D1', 'S8_D1', 'S9_D1', 'S10_D1']
last_chans = ['S1_D8', 'S2_D8', 'S3_D8', 'S4_D8', 'S5_D8', 'S6_D8', 'S7_D8', 'S8_D8', 'S9_D8', 'S10_D8']
assert mne_dc.info['ch_names'][:10] == [i_chan + ' ' + 'DC' for i_chan in first_chans]
assert mne_ac.info['ch_names'][:10] == [i_chan + ' ' + 'AC' for i_chan in first_chans]
assert mne_ph.info['ch_names'][:10] == [i_chan + ' ' + 'Ph' for i_chan in first_chans]
assert mne_dc.info['ch_names'][70:] == [i_chan + ' ' + 'DC' for i_chan in last_chans]
assert mne_ac.info['ch_names'][70:] == [i_chan + ' ' + 'AC' for i_chan in last_chans]
assert mne_ph.info['ch_names'][70:] == [i_chan + ' ' + 'Ph' for i_chan in last_chans]
assert len(raw.annotations) == 0
```

## Next Steps


---

*Source: test_boxy.py:69 | Complexity: Advanced | Last updated: 2026-05-18*