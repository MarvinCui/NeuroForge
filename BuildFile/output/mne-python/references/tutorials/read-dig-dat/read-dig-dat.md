# How To: Read Dig Dat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading *.dat electrode locations.

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

### Step 1: 'Test reading *.dat electrode locations.'

```python
'Test reading *.dat electrode locations.'
```

**Verification:**
```python
assert_allclose(target['O2']['r'], [0, 0.01, 0.02])
```

### Step 2: Assign rows = value

```python
rows = [['Nasion', 78, 0.0, 1.0, 0.0], ['Left', 76, -1.0, 0.0, 0.0], ['Right', 82, 1.0, -0.0, 0.0], ['O2', 69, -0.5, -0.9, 0.05], ['O2', 68, 0.0, 0.01, 0.02], ['Centroid', 67, 0.0, 0.0, 0.0]]
```

**Verification:**
```python
assert set(dig.ch_names) == {'O2'}
```

### Step 3: Assign fname_temp = value

```python
fname_temp = tmp_path / 'test.dat'
```

**Verification:**
```python
assert dig.dig == target
```

### Step 4: Assign idents = value

```python
idents = {78: FIFF.FIFFV_POINT_NASION, 76: FIFF.FIFFV_POINT_LPA, 82: FIFF.FIFFV_POINT_RPA, 68: 1, 69: 1}
```

### Step 5: Assign kinds = value

```python
kinds = {78: FIFF.FIFFV_POINT_CARDINAL, 76: FIFF.FIFFV_POINT_CARDINAL, 82: FIFF.FIFFV_POINT_CARDINAL, 69: FIFF.FIFFV_POINT_EEG, 68: FIFF.FIFFV_POINT_EEG}
```

### Step 6: Assign target = value

```python
target = {row[0]: {'r': row[2:], 'ident': idents[row[1]], 'kind': kinds[row[1]], 'coord_frame': 0} for row in rows[:-1]}
```

### Step 7: Call assert_allclose()

```python
assert_allclose(target['O2']['r'], [0, 0.01, 0.02])
```

**Verification:**
```python
assert set(dig.ch_names) == {'O2'}
```

### Step 8: Assign keys = chain(...)

```python
keys = chain(['Left', 'Nasion', 'Right'], dig.ch_names)
```

### Step 9: Assign target = value

```python
target = [target[k] for k in keys]
```

**Verification:**
```python
assert dig.dig == target
```

### Step 10: Assign dig = read_dig_dat(...)

```python
dig = read_dig_dat(fname_temp)
```

### Step 11: Assign name = unknown.rjust(...)

```python
name = row[0].rjust(10)
```

### Step 12: Assign data = unknown.join(...)

```python
data = '\t'.join(map(str, row[1:]))
```

### Step 13: Call fid.write()

```python
fid.write(f'{name}\t{data}\n')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading *.dat electrode locations.'
rows = [['Nasion', 78, 0.0, 1.0, 0.0], ['Left', 76, -1.0, 0.0, 0.0], ['Right', 82, 1.0, -0.0, 0.0], ['O2', 69, -0.5, -0.9, 0.05], ['O2', 68, 0.0, 0.01, 0.02], ['Centroid', 67, 0.0, 0.0, 0.0]]
fname_temp = tmp_path / 'test.dat'
with open(fname_temp, 'w') as fid:
    for row in rows:
        name = row[0].rjust(10)
        data = '\t'.join(map(str, row[1:]))
        fid.write(f'{name}\t{data}\n')
idents = {78: FIFF.FIFFV_POINT_NASION, 76: FIFF.FIFFV_POINT_LPA, 82: FIFF.FIFFV_POINT_RPA, 68: 1, 69: 1}
kinds = {78: FIFF.FIFFV_POINT_CARDINAL, 76: FIFF.FIFFV_POINT_CARDINAL, 82: FIFF.FIFFV_POINT_CARDINAL, 69: FIFF.FIFFV_POINT_EEG, 68: FIFF.FIFFV_POINT_EEG}
target = {row[0]: {'r': row[2:], 'ident': idents[row[1]], 'kind': kinds[row[1]], 'coord_frame': 0} for row in rows[:-1]}
assert_allclose(target['O2']['r'], [0, 0.01, 0.02])
with pytest.warns(RuntimeWarning, match='Duplic.*for O2 \\(2\\)'):
    dig = read_dig_dat(fname_temp)
assert set(dig.ch_names) == {'O2'}
keys = chain(['Left', 'Nasion', 'Right'], dig.ch_names)
target = [target[k] for k in keys]
assert dig.dig == target
```

## Next Steps


---

*Source: test_montage.py:647 | Complexity: Advanced | Last updated: 2026-05-18*