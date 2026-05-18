# How To: Snirf Nonstandard

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test custom tags.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `shutil`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`
- `shutil`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test custom tags.'

```python
'Test custom tags.'
```

**Verification:**
```python
assert raw.info['subject_info']['first_name'] == 'default'
```

### Step 2: Assign fname = value

```python
fname = str(tmp_path) + '/mod.snirf'
```

**Verification:**
```python
assert raw.info['subject_info']['first_name'] == 'W'
```

### Step 3: Call shutil.copy()

```python
shutil.copy(sfnirs_homer_103_wShort, fname)
```

**Verification:**
```python
assert raw.info['subject_info']['middle_name'] == 'X'
```

### Step 4: Call _chmod_rw_R()

```python
_chmod_rw_R(tmp_path)
```

**Verification:**
```python
assert raw.info['subject_info']['last_name'] == 'Y'
```

### Step 5: Assign raw = read_raw_snirf(...)

```python
raw = read_raw_snirf(fname, preload=True)
```

**Verification:**
```python
assert raw.info['subject_info']['sex'] == 1
```

### Step 6: Assign raw = read_raw_snirf(...)

```python
raw = read_raw_snirf(fname, preload=True)
```

**Verification:**
```python
assert raw.info['subject_info']['his_id'] == 'default'
```

### Step 7: Assign raw = read_raw_snirf(...)

```python
raw = read_raw_snirf(fname, preload=True)
```

**Verification:**
```python
assert raw.info['subject_info']['sex'] == 2
```

### Step 8: Assign raw = read_raw_snirf(...)

```python
raw = read_raw_snirf(fname, preload=True)
```

**Verification:**
```python
assert raw.info['subject_info']['sex'] == 0
```

### Step 9: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/middleName', data=[b'X'])
```

### Step 10: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/lastName', data=[b'Y'])
```

### Step 11: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/sex', data=[b'1'])
```

### Step 12: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/firstName', data=[b'W'])
```

### Step 13: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/sex', data=[b'2'])
```

### Step 14: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/sex', data=[b'0'])
```

### Step 15: Call f.create_dataset()

```python
f.create_dataset('nirs/metaDataTags/MNE_coordFrame', data=[1])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test custom tags.'
fname = str(tmp_path) + '/mod.snirf'
shutil.copy(sfnirs_homer_103_wShort, fname)
_chmod_rw_R(tmp_path)
with h5py.File(fname, 'r+') as f:
    f.create_dataset('nirs/metaDataTags/middleName', data=[b'X'])
    f.create_dataset('nirs/metaDataTags/lastName', data=[b'Y'])
    f.create_dataset('nirs/metaDataTags/sex', data=[b'1'])
raw = read_raw_snirf(fname, preload=True)
assert raw.info['subject_info']['first_name'] == 'default'
with h5py.File(fname, 'r+') as f:
    f.create_dataset('nirs/metaDataTags/firstName', data=[b'W'])
raw = read_raw_snirf(fname, preload=True)
assert raw.info['subject_info']['first_name'] == 'W'
assert raw.info['subject_info']['middle_name'] == 'X'
assert raw.info['subject_info']['last_name'] == 'Y'
assert raw.info['subject_info']['sex'] == 1
assert raw.info['subject_info']['his_id'] == 'default'
with h5py.File(fname, 'r+') as f:
    del f['nirs/metaDataTags/sex']
    f.create_dataset('nirs/metaDataTags/sex', data=[b'2'])
raw = read_raw_snirf(fname, preload=True)
assert raw.info['subject_info']['sex'] == 2
with h5py.File(fname, 'r+') as f:
    del f['nirs/metaDataTags/sex']
    f.create_dataset('nirs/metaDataTags/sex', data=[b'0'])
raw = read_raw_snirf(fname, preload=True)
assert raw.info['subject_info']['sex'] == 0
with h5py.File(fname, 'r+') as f:
    f.create_dataset('nirs/metaDataTags/MNE_coordFrame', data=[1])
```

## Next Steps


---

*Source: test_snirf.py:253 | Complexity: Advanced | Last updated: 2026-05-18*