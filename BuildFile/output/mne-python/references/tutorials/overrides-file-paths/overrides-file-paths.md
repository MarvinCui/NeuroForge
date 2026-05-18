# How To: Overrides File Paths

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: ``data_fname`` and ``marker_fname`` redirect the sibling file lookups.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `configparser`
- `datetime`
- `inspect`
- `re`
- `shutil`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: '``data_fname`` and ``marker_fname`` redirect the sibling file lookups.'

```python
'``data_fname`` and ``marker_fname`` redirect the sibling file lookups.'
```

**Verification:**
```python
assert raw.get_data().shape[0] == 32
```

### Step 2: Call shutil.copy()

```python
shutil.copy(vhdr_path, tmp_path / 'test.vhdr')
```

**Verification:**
```python
assert len(raw.annotations) > 0
```

### Step 3: Call shutil.copy()

```python
shutil.copy(eeg_path, tmp_path / 'renamed.eeg')
```

**Verification:**
```python
assert len(raw.annotations) == 0
```

### Step 4: Call shutil.copy()

```python
shutil.copy(vmrk_path, tmp_path / 'renamed.vmrk')
```

**Verification:**
```python
assert raw.info['meas_date'] is None
```

### Step 5: Assign use_vhdr = value

```python
use_vhdr = tmp_path / 'test.vhdr'
```

### Step 6: Assign overrides = value

```python
overrides = {'data_fname': 'renamed.eeg', 'marker_fname': 'renamed.vmrk'}
```

### Step 7: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(use_vhdr, overrides=overrides, preload=True)
```

**Verification:**
```python
assert raw.get_data().shape[0] == 32
```

### Step 8: Call unknown.unlink()

```python
(tmp_path / 'renamed.vmrk').unlink()
```

### Step 9: Assign raw = read_raw_brainvision(...)

```python
raw = read_raw_brainvision(use_vhdr, overrides={'data_fname': 'renamed.eeg', 'marker_fname': False})
```

**Verification:**
```python
assert len(raw.annotations) == 0
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'``data_fname`` and ``marker_fname`` redirect the sibling file lookups.'
shutil.copy(vhdr_path, tmp_path / 'test.vhdr')
shutil.copy(eeg_path, tmp_path / 'renamed.eeg')
shutil.copy(vmrk_path, tmp_path / 'renamed.vmrk')
use_vhdr = tmp_path / 'test.vhdr'
overrides = {'data_fname': 'renamed.eeg', 'marker_fname': 'renamed.vmrk'}
raw = read_raw_brainvision(use_vhdr, overrides=overrides, preload=True)
assert raw.get_data().shape[0] == 32
assert len(raw.annotations) > 0
(tmp_path / 'renamed.vmrk').unlink()
raw = read_raw_brainvision(use_vhdr, overrides={'data_fname': 'renamed.eeg', 'marker_fname': False})
assert len(raw.annotations) == 0
assert raw.info['meas_date'] is None
```

## Next Steps


---

*Source: test_brainvision.py:772 | Complexity: Advanced | Last updated: 2026-05-18*