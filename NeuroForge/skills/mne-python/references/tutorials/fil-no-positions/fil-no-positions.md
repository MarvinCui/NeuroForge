# How To: Fil No Positions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test FIL reader in cases where a position file is missing.

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

### Step 1: 'Test FIL reader in cases where a position file is missing.'

```python
'Test FIL reader in cases where a position file is missing.'
```

**Verification:**
```python
assert isnan(locs).all()
```

### Step 2: Assign test_path = value

```python
test_path = tmp_path / 'FIL'
```

### Step 3: Call copytree_rw()

```python
copytree_rw(fil_path, test_path)
```

### Step 4: Assign posname = value

```python
posname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_positions.tsv'
```

### Step 5: Assign binname = value

```python
binname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
```

### Step 6: Call remove()

```python
remove(posname)
```

### Step 7: Assign chs = value

```python
chs = raw.info['chs']
```

### Step 8: Assign locs = array(...)

```python
locs = array([ch['loc'][:] for ch in chs])
```

**Verification:**
```python
assert isnan(locs).all()
```

### Step 9: Assign raw = read_raw_fil(...)

```python
raw = read_raw_fil(binname)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test FIL reader in cases where a position file is missing.'
test_path = tmp_path / 'FIL'
copytree_rw(fil_path, test_path)
posname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_positions.tsv'
binname = test_path / 'sub-noise_ses-001_task-noise220622_run-001_meg.bin'
remove(posname)
with pytest.warns(RuntimeWarning, match='No sensor position.*'):
    raw = read_raw_fil(binname)
chs = raw.info['chs']
locs = array([ch['loc'][:] for ch in chs])
assert isnan(locs).all()
```

## Next Steps


---

*Source: test_fil.py:161 | Complexity: Advanced | Last updated: 2026-05-18*