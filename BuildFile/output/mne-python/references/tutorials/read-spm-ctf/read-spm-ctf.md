# How To: Read Spm Ctf

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test CTF reader with omitted samples.

## Prerequisites

**Required Modules:**
- `copy`
- `os`
- `shutil`
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy`
- `numpy.testing`
- `mne`
- `mne.io.ctf.info`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.io`
- `mne.io.ctf.constants`
- `mne.io.ctf.info`
- `mne.io.tests.test_raw`
- `mne.tests.test_annotations`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test CTF reader with omitted samples.'

```python
'Test CTF reader with omitted samples.'
```

**Verification:**
```python
assert extras['n_samp'] == raw.n_times
```

### Step 2: Assign raw_fname = op.join(...)

```python
raw_fname = op.join(spm_path, 'MEG', 'spm', 'SPM_CTF_MEG_example_faces1_3D.ds')
```

**Verification:**
```python
assert extras['n_samp'] != extras['n_samp_tot']
```

### Step 3: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(raw_fname)
```

**Verification:**
```python
assert np.all(coord_frames == FIFF.FIFFV_COORD_HEAD)
```

### Step 4: Assign extras = value

```python
extras = raw._raw_extras[0]
```

**Verification:**
```python
assert cardinals[1][0] < cardinals[2][0] < cardinals[3][0]
```

### Step 5: Assign coord_frames = np.array(...)

```python
coord_frames = np.array([d['coord_frame'] for d in raw.info['dig']])
```

**Verification:**
```python
assert cardinals[1][1] < cardinals[2][1]
```

### Step 6: Assign cardinals = value

```python
cardinals = {d['ident']: d['r'] for d in raw.info['dig']}
```

**Verification:**
```python
assert cardinals[3][1] < cardinals[2][1]
```

### Step 7: Call assert_allclose()

```python
assert_allclose(cardinals[key][2], 0, atol=1e-06)
```

**Verification:**
```python
assert_allclose(cardinals[key][2], 0, atol=1e-06)
```


## Complete Example

```python
# Workflow
'Test CTF reader with omitted samples.'
raw_fname = op.join(spm_path, 'MEG', 'spm', 'SPM_CTF_MEG_example_faces1_3D.ds')
raw = read_raw_ctf(raw_fname)
extras = raw._raw_extras[0]
assert extras['n_samp'] == raw.n_times
assert extras['n_samp'] != extras['n_samp_tot']
coord_frames = np.array([d['coord_frame'] for d in raw.info['dig']])
assert np.all(coord_frames == FIFF.FIFFV_COORD_HEAD)
cardinals = {d['ident']: d['r'] for d in raw.info['dig']}
assert cardinals[1][0] < cardinals[2][0] < cardinals[3][0]
assert cardinals[1][1] < cardinals[2][1]
assert cardinals[3][1] < cardinals[2][1]
for key in cardinals.keys():
    assert_allclose(cardinals[key][2], 0, atol=1e-06)
```

## Next Steps


---

*Source: test_ctf.py:344 | Complexity: Intermediate | Last updated: 2026-05-18*