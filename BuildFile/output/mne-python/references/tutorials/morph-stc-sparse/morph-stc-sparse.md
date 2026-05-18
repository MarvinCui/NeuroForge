# How To: Morph Stc Sparse

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test morphing stc with sparse=True.

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

### Step 1: 'Test morphing stc with sparse=True.'

```python
'Test morphing stc with sparse=True.'
```

**Verification:**
```python
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
```

### Step 2: Assign subject_from = 'sample'

```python
subject_from = 'sample'
```

**Verification:**
```python
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
```

### Step 3: Assign subject_to = 'fsaverage'

```python
subject_to = 'fsaverage'
```

**Verification:**
```python
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
```

### Step 4: Assign stc_from = read_source_estimate(...)

```python
stc_from = read_source_estimate(fname_smorph, subject='sample')
```

**Verification:**
```python
assert stc_to_sparse.subject == subject_to
```

### Step 5: Assign unknown = value

```python
stc_from.vertices[0] = stc_from.vertices[0][[100, 500]]
```

**Verification:**
```python
assert stc_from.tmin == stc_from.tmin
```

### Step 6: Assign unknown = value

```python
stc_from.vertices[1] = stc_from.vertices[1][[200]]
```

**Verification:**
```python
assert stc_from.tstep == stc_from.tstep
```

### Step 7: Assign stc_from._data = value

```python
stc_from._data = stc_from._data[:3]
```

**Verification:**
```python
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
```

### Step 8: Assign stc_to_sparse = compute_source_morph.apply(...)

```python
stc_to_sparse = compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
```

**Verification:**
```python
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
```

**Verification:**
```python
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
```

### Step 10: Assign unknown = np.array(...)

```python
stc_from.vertices[0] = np.array([], dtype=np.int64)
```

**Verification:**
```python
assert stc_to_sparse.subject == subject_to
```

### Step 11: Assign stc_from._data = value

```python
stc_from._data = stc_from._data[:1]
```

**Verification:**
```python
assert stc_from.tmin == stc_from.tmin
```

### Step 12: Assign stc_to_sparse = compute_source_morph.apply(...)

```python
stc_to_sparse = compute_source_morph(stc_from, subject_from, subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
```

**Verification:**
```python
assert stc_from.tstep == stc_from.tstep
```

### Step 13: Call assert_allclose()

```python
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
```

**Verification:**
```python
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
```

### Step 14: Call compute_source_morph()

```python
compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=5, sparse=True, subjects_dir=subjects_dir)
```

### Step 15: Call compute_source_morph()

```python
compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, xhemi=True, subjects_dir=subjects_dir)
```


## Complete Example

```python
# Workflow
'Test morphing stc with sparse=True.'
subject_from = 'sample'
subject_to = 'fsaverage'
stc_from = read_source_estimate(fname_smorph, subject='sample')
stc_from.vertices[0] = stc_from.vertices[0][[100, 500]]
stc_from.vertices[1] = stc_from.vertices[1][[200]]
stc_from._data = stc_from._data[:3]
stc_to_sparse = compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
assert stc_to_sparse.subject == subject_to
assert stc_from.tmin == stc_from.tmin
assert stc_from.tstep == stc_from.tstep
stc_from.vertices[0] = np.array([], dtype=np.int64)
stc_from._data = stc_from._data[:1]
stc_to_sparse = compute_source_morph(stc_from, subject_from, subject_to, spacing=None, sparse=True, subjects_dir=subjects_dir).apply(stc_from)
assert_allclose(np.sort(stc_from.data.sum(axis=1)), np.sort(stc_to_sparse.data.sum(axis=1)))
assert len(stc_from.rh_vertno) == len(stc_to_sparse.rh_vertno)
assert len(stc_from.lh_vertno) == len(stc_to_sparse.lh_vertno)
assert stc_to_sparse.subject == subject_to
assert stc_from.tmin == stc_from.tmin
assert stc_from.tstep == stc_from.tstep
with pytest.raises(ValueError, match='spacing must be set to None'):
    compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=5, sparse=True, subjects_dir=subjects_dir)
with pytest.raises(ValueError, match='xhemi=True can only be used with'):
    compute_source_morph(stc_from, subject_from=subject_from, subject_to=subject_to, spacing=None, sparse=True, xhemi=True, subjects_dir=subjects_dir)
```

## Next Steps


---

*Source: test_morph.py:831 | Complexity: Advanced | Last updated: 2026-05-18*