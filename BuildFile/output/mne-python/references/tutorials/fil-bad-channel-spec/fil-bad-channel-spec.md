# How To: Fil Bad Channel Spec

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test FIL reader when a bad channel is specified in channels.tsv.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `scipy.io`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.io.fil.sensors`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test FIL reader when a bad channel is specified in channels.tsv.'

```python
'Test FIL reader when a bad channel is specified in channels.tsv.'
```

**Verification:**
```python
assert bad_chan in bads
```

### Step 2: Assign test_path = value

```python
test_path = tmp_path / 'FIL'
```

### Step 3: Call copytree_rw()

```python
copytree_rw(fil_path, test_path)
```

### Step 4: Assign channame = value

```python
channame = test_path / 'sub-noise_ses-001_task-noise220622_run-001_channels.tsv'
```

### Step 5: Assign binname = value

```python
binname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
```

### Step 6: Assign bad_chan = 'G2-OG-Y'

```python
bad_chan = 'G2-OG-Y'
```

### Step 7: Call _set_bads_tsv()

```python
_set_bads_tsv(channame, bad_chan)
```

### Step 8: Assign raw = read_raw_fil(...)

```python
raw = read_raw_fil(binname)
```

### Step 9: Assign bads = value

```python
bads = raw.info['bads']
```

**Verification:**
```python
assert bad_chan in bads
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test FIL reader when a bad channel is specified in channels.tsv.'
test_path = tmp_path / 'FIL'
copytree_rw(fil_path, test_path)
channame = test_path / 'sub-noise_ses-001_task-noise220622_run-001_channels.tsv'
binname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
bad_chan = 'G2-OG-Y'
_set_bads_tsv(channame, bad_chan)
raw = read_raw_fil(binname)
bads = raw.info['bads']
assert bad_chan in bads
```

## Next Steps


---

*Source: test_fil.py:179 | Complexity: Advanced | Last updated: 2026-05-18*