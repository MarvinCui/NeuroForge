# How To: Read Dig Polhemus Isotrak Error Handling

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test errors in reading Polhemus IsoTrak files.

1 - matching ch_names and number of points in isotrak file.
2 - error for unsupported file extensions.

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
# Fixtures: isotrak_eeg, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test errors in reading Polhemus IsoTrak files.\n\n    1 - matching ch_names and number of points in isotrak file.\n    2 - error for unsupported file extensions.\n    '

```python
'Test errors in reading Polhemus IsoTrak files.\n\n    1 - matching ch_names and number of points in isotrak file.\n    2 - error for unsupported file extensions.\n    '
```

### Step 2: Assign N_CHANNELS = 5

```python
N_CHANNELS = 5
```

### Step 3: Assign EXPECTED_ERR_MSG = 'not match the number of points.*Expected.*5, given 47'

```python
EXPECTED_ERR_MSG = 'not match the number of points.*Expected.*5, given 47'
```

### Step 4: Assign fname = value

```python
fname = tmp_path / 'test.bar'
```

### Step 5: Call shutil.copyfile()

```python
shutil.copyfile(isotrak_eeg, fname)
```

### Step 6: Assign _ = read_dig_polhemus_isotrak(...)

```python
_ = read_dig_polhemus_isotrak(fname=isotrak_eeg, ch_names=[f'eeg {ii:01d}' for ii in range(N_CHANNELS + 42)])
```

### Step 7: Assign _ = read_dig_polhemus_isotrak(...)

```python
_ = read_dig_polhemus_isotrak(fname=fname, ch_names=None)
```


## Complete Example

```python
# Setup
# Fixtures: isotrak_eeg, tmp_path

# Workflow
'Test errors in reading Polhemus IsoTrak files.\n\n    1 - matching ch_names and number of points in isotrak file.\n    2 - error for unsupported file extensions.\n    '
N_CHANNELS = 5
EXPECTED_ERR_MSG = 'not match the number of points.*Expected.*5, given 47'
with pytest.raises(ValueError, match=EXPECTED_ERR_MSG):
    _ = read_dig_polhemus_isotrak(fname=isotrak_eeg, ch_names=[f'eeg {ii:01d}' for ii in range(N_CHANNELS + 42)])
fname = tmp_path / 'test.bar'
shutil.copyfile(isotrak_eeg, fname)
with pytest.raises(ValueError, match="Allowed val.*'.hsp', '.elp', and '.eeg', but got '.bar' instead"):
    _ = read_dig_polhemus_isotrak(fname=fname, ch_names=None)
```

## Next Steps


---

*Source: test_montage.py:854 | Complexity: Intermediate | Last updated: 2026-05-18*