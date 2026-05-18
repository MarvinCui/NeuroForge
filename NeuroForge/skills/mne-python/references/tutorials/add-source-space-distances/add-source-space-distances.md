# How To: Add Source Space Distances

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test adding distances to source space.

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

### Step 1: 'Test adding distances to source space.'

```python
'Test adding distances to source space.'
```

**Verification:**
```python
assert n_do % n_jobs != 0
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname)
```

**Verification:**
```python
assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
```

### Step 3: Assign src_new = read_source_spaces(...)

```python
src_new = read_source_spaces(fname)
```

**Verification:**
```python
assert_array_equal(sn['dist_limit'], np.array([np.inf], np.float32))
```

### Step 4: Assign n_do = 19

```python
n_do = 19
```

**Verification:**
```python
assert np.sum(ds[0].data < 0.007) > 10
```

### Step 5: Assign unknown = unknown.copy(...)

```python
src_new[0]['vertno'] = src_new[0]['vertno'][:n_do].copy()
```

**Verification:**
```python
assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-09)
```

### Step 6: Assign unknown = unknown.copy(...)

```python
src_new[1]['vertno'] = src_new[1]['vertno'][:n_do].copy()
```

### Step 7: Assign out_name = value

```python
out_name = tmp_path / 'temp-src.fif'
```

### Step 8: Assign n_jobs = 2

```python
n_jobs = 2
```

**Verification:**
```python
assert n_do % n_jobs != 0
```

### Step 9: Call add_source_space_distances()

```python
add_source_space_distances(src_new, n_jobs=n_jobs)
```

### Step 10: Call write_source_spaces()

```python
write_source_spaces(out_name, src_new)
```

### Step 11: Assign src_new = read_source_spaces(...)

```python
src_new = read_source_spaces(out_name)
```

### Step 12: Call add_source_space_distances()

```python
add_source_space_distances(src_new, dist_limit=-1)
```

### Step 13: Assign v = value

```python
v = so['vertno'][:n_do]
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(sn['dist_limit'], np.array([np.inf], np.float32))
```

### Step 16: Assign do = value

```python
do = so['dist']
```

### Step 17: Assign dn = value

```python
dn = sn['dist']
```

### Step 18: Assign ds = list(...)

```python
ds = list()
```

**Verification:**
```python
assert np.sum(ds[0].data < 0.007) > 10
```

### Step 19: Assign d = value

```python
d = ds[0] - ds[1]
```

### Step 20: Call assert_allclose()

```python
assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-09)
```

### Step 21: Assign unknown = 0

```python
d.data[d.data > 0.007] = 0
```

### Step 22: Assign d = value

```python
d = d[v][:, v]
```

### Step 23: Call d.eliminate_zeros()

```python
d.eliminate_zeros()
```

### Step 24: Call ds.append()

```python
ds.append(d)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test adding distances to source space.'
src = read_source_spaces(fname)
src_new = read_source_spaces(fname)
del src_new[0]['dist']
del src_new[1]['dist']
n_do = 19
src_new[0]['vertno'] = src_new[0]['vertno'][:n_do].copy()
src_new[1]['vertno'] = src_new[1]['vertno'][:n_do].copy()
out_name = tmp_path / 'temp-src.fif'
n_jobs = 2
assert n_do % n_jobs != 0
with pytest.raises(ValueError, match='non-negative'):
    add_source_space_distances(src_new, dist_limit=-1)
add_source_space_distances(src_new, n_jobs=n_jobs)
write_source_spaces(out_name, src_new)
src_new = read_source_spaces(out_name)
for so, sn in zip(src, src_new):
    v = so['vertno'][:n_do]
    assert_array_equal(so['dist_limit'], np.array([-0.007], np.float32))
    assert_array_equal(sn['dist_limit'], np.array([np.inf], np.float32))
    do = so['dist']
    dn = sn['dist']
    ds = list()
    for d in [do, dn]:
        d.data[d.data > 0.007] = 0
        d = d[v][:, v]
        d.eliminate_zeros()
        ds.append(d)
    assert np.sum(ds[0].data < 0.007) > 10
    d = ds[0] - ds[1]
    assert_allclose(np.zeros_like(d.data), d.data, rtol=0, atol=1e-09)
```

## Next Steps


---

*Source: test_source_space.py:232 | Complexity: Advanced | Last updated: 2026-05-18*