# How To: Read Dig Montage Using Polhemus Fastscan Error Handling

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading Polhemus FastSCAN errors.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading Polhemus FastSCAN errors.'

```python
'Test reading Polhemus FastSCAN errors.'
```

### Step 2: Assign fname = value

```python
fname = tmp_path / 'faulty_FastSCAN.txt'
```

### Step 3: Assign fname = value

```python
fname = tmp_path / 'faulty_FastSCAN.bar'
```

### Step 4: Assign EXPECTED_ERR_MSG = "allowed value is '.txt', but got '.bar' instead"

```python
EXPECTED_ERR_MSG = "allowed value is '.txt', but got '.bar' instead"
```

### Step 5: Assign content = fid.read.replace(...)

```python
content = fid.read().replace('FastSCAN', 'XxxxXXXX')
```

### Step 6: Call fid.write()

```python
fid.write(content)
```

### Step 7: Assign _ = read_polhemus_fastscan(...)

```python
_ = read_polhemus_fastscan(fname)
```

### Step 8: Call fid.write()

```python
fid.write(content)
```

### Step 9: Assign _ = read_polhemus_fastscan(...)

```python
_ = read_polhemus_fastscan(fname=fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading Polhemus FastSCAN errors.'
with open(kit_dir / 'test_elp.txt') as fid:
    content = fid.read().replace('FastSCAN', 'XxxxXXXX')
fname = tmp_path / 'faulty_FastSCAN.txt'
with open(fname, 'w') as fid:
    fid.write(content)
with pytest.raises(ValueError, match='not contain.*Polhemus FastSCAN'):
    _ = read_polhemus_fastscan(fname)
fname = tmp_path / 'faulty_FastSCAN.bar'
with open(fname, 'w') as fid:
    fid.write(content)
EXPECTED_ERR_MSG = "allowed value is '.txt', but got '.bar' instead"
with pytest.raises(ValueError, match=EXPECTED_ERR_MSG):
    _ = read_polhemus_fastscan(fname=fname)
```

## Next Steps


---

*Source: test_montage.py:734 | Complexity: Advanced | Last updated: 2026-05-18*