# How To: Unknown Format

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test our warning about an unknown format.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `scipy.io`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.kit.constants`
- `mne.io.kit.coreg`
- `mne.io.kit.kit`
- `mne.io.tests.test_raw`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test our warning about an unknown format.'

```python
'Test our warning about an unknown format.'
```

**Verification:**
```python
assert version > 2
```

### Step 2: Assign fname = value

```python
fname = tmp_path / ricoh_path.name
```

### Step 3: Assign unknown = get_kit_info(...)

```python
_, kit_info = get_kit_info(ricoh_path, allow_unknown_format=False)
```

### Step 4: Assign n_before = value

```python
n_before = kit_info['dirs'][KIT.DIR_INDEX_SYSTEM]['offset']
```

### Step 5: Call read_raw_kit()

```python
read_raw_kit(fname)
```

### Step 6: Call fout.write()

```python
fout.write(fin.read(n_before))
```

### Step 7: Assign unknown = np.fromfile(...)

```python
version, revision = np.fromfile(fin, '<i4', 2)
```

**Verification:**
```python
assert version > 2
```

### Step 8: Assign version = 1

```python
version = 1
```

### Step 9: Call np.array.tofile()

```python
np.array([version, revision], '<i4').tofile(fout)
```

### Step 10: Call fout.write()

```python
fout.write(fin.read())
```

### Step 11: Call read_raw_kit()

```python
read_raw_kit(fname, allow_unknown_format=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test our warning about an unknown format.'
fname = tmp_path / ricoh_path.name
_, kit_info = get_kit_info(ricoh_path, allow_unknown_format=False)
n_before = kit_info['dirs'][KIT.DIR_INDEX_SYSTEM]['offset']
with open(fname, 'wb') as fout:
    with open(ricoh_path, 'rb') as fin:
        fout.write(fin.read(n_before))
        version, revision = np.fromfile(fin, '<i4', 2)
        assert version > 2
        version = 1
        np.array([version, revision], '<i4').tofile(fout)
        fout.write(fin.read())
with pytest.raises(ValueError, match='SQD file format V1R000 is not offi'):
    read_raw_kit(fname)
with pytest.raises(Exception):
    with pytest.warns(RuntimeWarning, match='Force loading'):
        read_raw_kit(fname, allow_unknown_format=True)
```

## Next Steps


---

*Source: test_kit.py:199 | Complexity: Advanced | Last updated: 2026-05-18*