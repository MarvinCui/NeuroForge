# How To: Dig Montage Trans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test getting a trans from and applying a trans to a montage.

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

### Step 1: 'Test getting a trans from and applying a trans to a montage.'

```python
'Test getting a trans from and applying a trans to a montage.'
```

**Verification:**
```python
assert montage.get_positions()['coord_frame'] == 'head'
```

### Step 2: Assign unknown = np.random.RandomState.randn(...)

```python
nasion, lpa, rpa, *ch_pos = np.random.RandomState(0).randn(10, 3)
```

**Verification:**
```python
assert str(position1) == str(position2)
```

### Step 3: Assign ch_pos = value

```python
ch_pos = {f'EEG{ii:3d}': pos for ii, pos in enumerate(ch_pos, 1)}
```

### Step 4: Assign montage = make_dig_montage(...)

```python
montage = make_dig_montage(ch_pos, nasion=nasion, lpa=lpa, rpa=rpa, coord_frame='mri')
```

### Step 5: Assign trans = compute_native_head_t(...)

```python
trans = compute_native_head_t(montage)
```

### Step 6: Call _ensure_trans()

```python
_ensure_trans(trans)
```

### Step 7: Assign fname = value

```python
fname = tmp_path / 'temp-mon.fif'
```

### Step 8: Assign position1 = montage.get_positions(...)

```python
position1 = montage.get_positions()
```

### Step 9: Call montage.apply_trans()

```python
montage.apply_trans(trans)
```

**Verification:**
```python
assert montage.get_positions()['coord_frame'] == 'head'
```

### Step 10: Call montage.apply_trans()

```python
montage.apply_trans(invert_transform(trans))
```

### Step 11: Assign position2 = montage.get_positions(...)

```python
position2 = montage.get_positions()
```

**Verification:**
```python
assert str(position1) == str(position2)
```

### Step 12: Call _check_roundtrip()

```python
_check_roundtrip(montage, fname, 'mri')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test getting a trans from and applying a trans to a montage.'
nasion, lpa, rpa, *ch_pos = np.random.RandomState(0).randn(10, 3)
ch_pos = {f'EEG{ii:3d}': pos for ii, pos in enumerate(ch_pos, 1)}
montage = make_dig_montage(ch_pos, nasion=nasion, lpa=lpa, rpa=rpa, coord_frame='mri')
trans = compute_native_head_t(montage)
_ensure_trans(trans)
fname = tmp_path / 'temp-mon.fif'
with pytest.warns(RuntimeWarning, match='MNE naming conventions'):
    _check_roundtrip(montage, fname, 'mri')
position1 = montage.get_positions()
montage.apply_trans(trans)
assert montage.get_positions()['coord_frame'] == 'head'
montage.apply_trans(invert_transform(trans))
position2 = montage.get_positions()
assert str(position1) == str(position2)
```

## Next Steps


---

*Source: test_montage.py:133 | Complexity: Advanced | Last updated: 2026-05-18*