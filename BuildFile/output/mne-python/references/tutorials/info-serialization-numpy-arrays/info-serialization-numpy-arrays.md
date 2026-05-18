# How To: Info Serialization Numpy Arrays

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that numpy arrays (e.g., compensation matrices) serialize correctly.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test that numpy arrays (e.g., compensation matrices) serialize correctly.'

```python
'Test that numpy arrays (e.g., compensation matrices) serialize correctly.'
```

**Verification:**
```python
assert len(info['comps']) > 0, 'CTF data should have compensation matrices'
```

### Step 2: Assign raw = read_raw_ctf(...)

```python
raw = read_raw_ctf(ctf_fname, preload=False, verbose=False)
```

**Verification:**
```python
assert 'data' in comp
```

### Step 3: Assign info = raw.info.copy(...)

```python
info = raw.info.copy()
```

**Verification:**
```python
assert 'data' in comp['data']
```

### Step 4: Assign json_path = value

```python
json_path = tmp_path / 'info_with_comps.json'
```

**Verification:**
```python
assert isinstance(comp_matrix, np.ndarray), 'Compensation matrix should be numpy array'
```

### Step 5: Assign info_restored = Info.from_json_dict(...)

```python
info_restored = Info.from_json_dict(info_dict)
```

**Verification:**
```python
assert comp_matrix.ndim == 2, 'Compensation matrix should be 2D'
```

### Step 6: Call assert_object_equal()

```python
assert_object_equal(info, info_restored)
```

**Verification:**
```python
assert comp_matrix.shape[0] > 0 and comp_matrix.shape[1] > 0
```

### Step 7: Assign comp_matrix = value

```python
comp_matrix = comp['data']['data']
```

**Verification:**
```python
assert len(info_restored['comps']) == len(info['comps'])
```

### Step 8: Call json.dump()

```python
json.dump(info.to_json_dict(), f)
```

**Verification:**
```python
assert isinstance(rest_matrix, np.ndarray)
```

### Step 9: Assign info_dict = json.load(...)

```python
info_dict = json.load(f)
```

**Verification:**
```python
assert rest_matrix.shape == orig_matrix.shape
```

### Step 10: Assign orig_matrix = value

```python
orig_matrix = orig_comp['data']['data']
```

**Verification:**
```python
assert rest_matrix.ndim == 2
```

### Step 11: Assign rest_matrix = value

```python
rest_matrix = rest_comp['data']['data']
```

**Verification:**
```python
assert_allclose(rest_matrix, orig_matrix, rtol=1e-10)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(rest_matrix, orig_matrix, rtol=1e-10)
```

**Verification:**
```python
assert orig_comp['data']['row_names'] == rest_comp['data']['row_names']
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test that numpy arrays (e.g., compensation matrices) serialize correctly.'
raw = read_raw_ctf(ctf_fname, preload=False, verbose=False)
info = raw.info.copy()
assert len(info['comps']) > 0, 'CTF data should have compensation matrices'
for comp in info['comps']:
    assert 'data' in comp
    assert 'data' in comp['data']
    comp_matrix = comp['data']['data']
    assert isinstance(comp_matrix, np.ndarray), 'Compensation matrix should be numpy array'
    assert comp_matrix.ndim == 2, 'Compensation matrix should be 2D'
    assert comp_matrix.shape[0] > 0 and comp_matrix.shape[1] > 0
json_path = tmp_path / 'info_with_comps.json'
with open(json_path, 'w') as f:
    json.dump(info.to_json_dict(), f)
with open(json_path) as f:
    info_dict = json.load(f)
info_restored = Info.from_json_dict(info_dict)
assert len(info_restored['comps']) == len(info['comps'])
for orig_comp, rest_comp in zip(info['comps'], info_restored['comps']):
    orig_matrix = orig_comp['data']['data']
    rest_matrix = rest_comp['data']['data']
    assert isinstance(rest_matrix, np.ndarray)
    assert rest_matrix.shape == orig_matrix.shape
    assert rest_matrix.ndim == 2
    assert_allclose(rest_matrix, orig_matrix, rtol=1e-10)
    assert orig_comp['data']['row_names'] == rest_comp['data']['row_names']
    assert orig_comp['data']['col_names'] == rest_comp['data']['col_names']
assert_object_equal(info, info_restored)
```

## Next Steps


---

*Source: test_meas_info.py:434 | Complexity: Advanced | Last updated: 2026-05-18*