# How To: Sparse Morph

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test sparse morphing.

## Prerequisites

**Required Modules:**
- `inspect`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.sparse`
- `scipy.sparse`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._freesurfer`
- `mne.datasets`
- `mne.fixes`
- `mne.minimum_norm`
- `mne.source_space._source_space`
- `mne.transforms`
- `mne.utils`
- `nibabel.processing`
- `nibabel.processing`
- `nibabel.spatialimages`
- `dipy.align.imaffine`


## Step-by-Step Guide

### Step 1: 'Test sparse morphing.'

```python
'Test sparse morphing.'
```

**Verification:**
```python
assert_array_less(dists[np.arange(len(order)), order], 1.5)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(stc_fs.data, stc_sample.data[np.concatenate(orders)])
```

### Step 3: Assign vertices_fs = value

```python
vertices_fs = [np.sort(rng.permutation(np.arange(10242))[:4]), np.sort(rng.permutation(np.arange(10242))[:6])]
```

**Verification:**
```python
assert_array_less(dists[np.arange(len(order)), order], 1.5)
```

### Step 4: Assign data = rng.randn(...)

```python
data = rng.randn(10, 1)
```

**Verification:**
```python
assert_allclose(stc_fs.data, stc_fs_return.data[np.concatenate(orders)])
```

### Step 5: Assign stc_fs = SourceEstimate(...)

```python
stc_fs = SourceEstimate(data, vertices_fs, 1, 1, 'fsaverage')
```

### Step 6: Assign spheres_fs = value

```python
spheres_fs = [mne.read_surface(subjects_dir / 'fsaverage' / 'surf' / f'{hemi}.sphere.reg')[0] for hemi in ('lh', 'rh')]
```

### Step 7: Assign spheres_sample = value

```python
spheres_sample = [mne.read_surface(subjects_dir / 'sample' / 'surf' / f'{hemi}.sphere.reg')[0] for hemi in ('lh', 'rh')]
```

### Step 8: Assign morph_fs_sample = compute_source_morph(...)

```python
morph_fs_sample = compute_source_morph(stc_fs, 'fsaverage', 'sample', sparse=True, spacing=None, subjects_dir=subjects_dir)
```

### Step 9: Assign stc_sample = morph_fs_sample.apply(...)

```python
stc_sample = morph_fs_sample.apply(stc_fs)
```

### Step 10: Assign offset = 0

```python
offset = 0
```

### Step 11: Assign orders = list(...)

```python
orders = list()
```

### Step 12: Call assert_allclose()

```python
assert_allclose(stc_fs.data, stc_sample.data[np.concatenate(orders)])
```

### Step 13: Assign morph_sample_fs = compute_source_morph(...)

```python
morph_sample_fs = compute_source_morph(stc_sample, 'sample', 'fsaverage', sparse=True, spacing=None, subjects_dir=subjects_dir)
```

### Step 14: Assign stc_fs_return = morph_sample_fs.apply(...)

```python
stc_fs_return = morph_sample_fs.apply(stc_sample)
```

### Step 15: Assign offset = 0

```python
offset = 0
```

### Step 16: Assign orders = list(...)

```python
orders = list()
```

### Step 17: Call assert_allclose()

```python
assert_allclose(stc_fs.data, stc_fs_return.data[np.concatenate(orders)])
```

### Step 18: Assign dists = cdist(...)

```python
dists = cdist(s1[v1], s2[v2])
```

### Step 19: Assign order = np.argmin(...)

```python
order = np.argmin(dists, axis=-1)
```

### Step 20: Call assert_array_less()

```python
assert_array_less(dists[np.arange(len(order)), order], 1.5)
```

### Step 21: Call orders.append()

```python
orders.append(order + offset)
```

### Step 22: Assign dists = cdist(...)

```python
dists = cdist(s[v1], s[v2])
```

### Step 23: Assign order = np.argmin(...)

```python
order = np.argmin(dists, axis=-1)
```

### Step 24: Call assert_array_less()

```python
assert_array_less(dists[np.arange(len(order)), order], 1.5)
```

### Step 25: Call orders.append()

```python
orders.append(order + offset)
```


## Complete Example

```python
# Workflow
'Test sparse morphing.'
rng = np.random.RandomState(0)
vertices_fs = [np.sort(rng.permutation(np.arange(10242))[:4]), np.sort(rng.permutation(np.arange(10242))[:6])]
data = rng.randn(10, 1)
stc_fs = SourceEstimate(data, vertices_fs, 1, 1, 'fsaverage')
spheres_fs = [mne.read_surface(subjects_dir / 'fsaverage' / 'surf' / f'{hemi}.sphere.reg')[0] for hemi in ('lh', 'rh')]
spheres_sample = [mne.read_surface(subjects_dir / 'sample' / 'surf' / f'{hemi}.sphere.reg')[0] for hemi in ('lh', 'rh')]
morph_fs_sample = compute_source_morph(stc_fs, 'fsaverage', 'sample', sparse=True, spacing=None, subjects_dir=subjects_dir)
stc_sample = morph_fs_sample.apply(stc_fs)
offset = 0
orders = list()
for v1, s1, v2, s2 in zip(stc_fs.vertices, spheres_fs, stc_sample.vertices, spheres_sample):
    dists = cdist(s1[v1], s2[v2])
    order = np.argmin(dists, axis=-1)
    assert_array_less(dists[np.arange(len(order)), order], 1.5)
    orders.append(order + offset)
    offset += len(order)
assert_allclose(stc_fs.data, stc_sample.data[np.concatenate(orders)])
morph_sample_fs = compute_source_morph(stc_sample, 'sample', 'fsaverage', sparse=True, spacing=None, subjects_dir=subjects_dir)
stc_fs_return = morph_sample_fs.apply(stc_sample)
offset = 0
orders = list()
for v1, s, v2 in zip(stc_fs.vertices, spheres_fs, stc_fs_return.vertices):
    dists = cdist(s[v1], s[v2])
    order = np.argmin(dists, axis=-1)
    assert_array_less(dists[np.arange(len(order)), order], 1.5)
    orders.append(order + offset)
    offset += len(order)
assert_allclose(stc_fs.data, stc_fs_return.data[np.concatenate(orders)])
```

## Next Steps


---

*Source: test_morph.py:81 | Complexity: Advanced | Last updated: 2026-05-18*