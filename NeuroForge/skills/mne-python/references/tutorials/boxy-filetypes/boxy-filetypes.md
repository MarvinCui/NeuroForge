# How To: Boxy Filetypes

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading parsed and unparsed BOXY data files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test reading parsed and unparsed BOXY data files.'

```python
'Test reading parsed and unparsed BOXY data files.'
```

**Verification:**
```python
assert raw.info['sfreq'] == 79.4722
```

### Step 2: Assign raw = read_raw_boxy(...)

```python
raw = read_raw_boxy(fname, verbose=True)
```

**Verification:**
```python
assert unp_dc.info['ch_names'] == [i_chan + ' ' + 'DC' for i_chan in chans]
```

### Step 3: Call _assert_ppod()

```python
_assert_ppod(raw, p_pod_0_84)
```

**Verification:**
```python
assert unp_ac.info['ch_names'] == [i_chan + ' ' + 'AC' for i_chan in chans]
```

### Step 4: Assign unp_dc = raw.copy.pick(...)

```python
unp_dc = raw.copy().pick('fnirs_cw_amplitude')
```

**Verification:**
```python
assert unp_ph.info['ch_names'] == [i_chan + ' ' + 'Ph' for i_chan in chans]
```

### Step 5: Assign unp_ac = raw.copy.pick(...)

```python
unp_ac = raw.copy().pick('fnirs_fd_ac_amplitude')
```

### Step 6: Assign unp_ph = raw.copy.pick(...)

```python
unp_ph = raw.copy().pick('fnirs_fd_phase')
```

### Step 7: Assign chans = value

```python
chans = ['S1_D1', 'S2_D1', 'S3_D1', 'S4_D1', 'S5_D1', 'S6_D1', 'S7_D1', 'S8_D1']
```

**Verification:**
```python
assert unp_dc.info['ch_names'] == [i_chan + ' ' + 'DC' for i_chan in chans]
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test reading parsed and unparsed BOXY data files.'
raw = read_raw_boxy(fname, verbose=True)
assert raw.info['sfreq'] == 79.4722
_assert_ppod(raw, p_pod_0_84)
unp_dc = raw.copy().pick('fnirs_cw_amplitude')
unp_ac = raw.copy().pick('fnirs_fd_ac_amplitude')
unp_ph = raw.copy().pick('fnirs_fd_phase')
chans = ['S1_D1', 'S2_D1', 'S3_D1', 'S4_D1', 'S5_D1', 'S6_D1', 'S7_D1', 'S8_D1']
assert unp_dc.info['ch_names'] == [i_chan + ' ' + 'DC' for i_chan in chans]
assert unp_ac.info['ch_names'] == [i_chan + ' ' + 'AC' for i_chan in chans]
assert unp_ph.info['ch_names'] == [i_chan + ' ' + 'Ph' for i_chan in chans]
```

## Next Steps


---

*Source: test_boxy.py:133 | Complexity: Intermediate | Last updated: 2026-05-18*