# How To: Add Source Space Distances Limited

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test adding distances to source space with a dist_limit.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test adding distances to source space with a dist_limit.'

```python
'Test adding distances to source space with a dist_limit.'
```

**Verification:**
```python
assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname)
```

**Verification:**
```python
assert_array_equal(sn['dist_limit'], np.array([0.007], np.float32))
```

### Step 3: Assign src_new = read_source_spaces(...)

```python
src_new = read_source_spaces(fname)
```

**Verification:**
```python
assert np.sum(do.data < 0.007) > 400
```

### Step 4: Assign n_do = 200

```python
n_do = 200
```

**Verification:**
```python
assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-06)
```

### Step 5: Assign unknown = unknown.copy(...)

```python
src_new[0]['vertno'] = src_new[0]['vertno'][:n_do].copy()
```

### Step 6: Assign unknown = unknown.copy(...)

```python
src_new[1]['vertno'] = src_new[1]['vertno'][:n_do].copy()
```

### Step 7: Assign out_name = value

```python
out_name = tmp_path / 'temp-src.fif'
```

### Step 8: Call add_source_space_distances()

```python
add_source_space_distances(src_new, dist_limit=0.007)
```

### Step 9: Call write_source_spaces()

```python
write_source_spaces(out_name, src_new)
```

### Step 10: Assign src_new = read_source_spaces(...)

```python
src_new = read_source_spaces(out_name)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(sn['dist_limit'], np.array([0.007], np.float32))
```

### Step 13: Assign do = value

```python
do = so['dist']
```

### Step 14: Assign dn = value

```python
dn = sn['dist']
```

### Step 15: Assign unknown = 0

```python
do.data[do.data > 0.007] = 0
```

### Step 16: Call do.eliminate_zeros()

```python
do.eliminate_zeros()
```

**Verification:**
```python
assert np.sum(do.data < 0.007) > 400
```

### Step 17: Assign d = value

```python
d = (do - dn)[:sn['vertno'][n_do - 1]][:, :sn['vertno'][n_do - 1]]
```

### Step 18: Call assert_allclose()

```python
assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-06)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test adding distances to source space with a dist_limit.'
src = read_source_spaces(fname)
src_new = read_source_spaces(fname)
del src_new[0]['dist']
del src_new[1]['dist']
n_do = 200
src_new[0]['vertno'] = src_new[0]['vertno'][:n_do].copy()
src_new[1]['vertno'] = src_new[1]['vertno'][:n_do].copy()
out_name = tmp_path / 'temp-src.fif'
add_source_space_distances(src_new, dist_limit=0.007)
write_source_spaces(out_name, src_new)
src_new = read_source_spaces(out_name)
for so, sn in zip(src, src_new):
    assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
    assert_array_equal(sn['dist_limit'], np.array([0.007], np.float32))
    do = so['dist']
    dn = sn['dist']
    do.data[do.data > 0.007] = 0
    do.eliminate_zeros()
    assert np.sum(do.data < 0.007) > 400
    d = (do - dn)[:sn['vertno'][n_do - 1]][:, :sn['vertno'][n_do - 1]]
    assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-06)
```

## Next Steps


---

*Source: test_source_space.py:198 | Complexity: Advanced | Last updated: 2026-05-18*