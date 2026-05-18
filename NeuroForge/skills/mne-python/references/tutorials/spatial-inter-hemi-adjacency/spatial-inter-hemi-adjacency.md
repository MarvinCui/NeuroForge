# How To: Spatial Inter Hemi Adjacency

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test spatial adjacency between hemispheres.

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `contextlib`
- `copy`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy`
- `scipy.optimize`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.morph_map`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test spatial adjacency between hemispheres.'

```python
'Test spatial adjacency between hemispheres.'
```

**Verification:**
```python
assert_equal(conn.data.size, 0)
```

### Step 2: Assign conn = spatial_inter_hemi_adjacency(...)

```python
conn = spatial_inter_hemi_adjacency(fname_src_3, 5e-06)
```

**Verification:**
```python
assert_equal(conn.data.size, np.prod(conn.shape) // 2)
```

### Step 3: Call assert_equal()

```python
assert_equal(conn.data.size, 0)
```

**Verification:**
```python
assert n_src * 0.02 < conn.data.size < n_src * 0.1
```

### Step 4: Assign conn = spatial_inter_hemi_adjacency(...)

```python
conn = spatial_inter_hemi_adjacency(fname_src_3, 5000000.0)
```

**Verification:**
```python
assert_equal(conn[:src[0]['nuse'], :src[0]['nuse']].data.size, 0)
```

### Step 5: Call assert_equal()

```python
assert_equal(conn.data.size, np.prod(conn.shape) // 2)
```

**Verification:**
```python
assert_equal(conn[-src[1]['nuse']:, -src[1]['nuse']:].data.size, 0)
```

### Step 6: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_src_3)
```

**Verification:**
```python
assert_equal(c.data.size, 0)
```

### Step 7: Assign conn = spatial_inter_hemi_adjacency(...)

```python
conn = spatial_inter_hemi_adjacency(src, 0.01)
```

**Verification:**
```python
assert_equal(upper_right.sum(), conn.sum() // 2)
```

### Step 8: Assign conn = conn.tocsr(...)

```python
conn = conn.tocsr()
```

**Verification:**
```python
assert set(use_labels) - set(good_labels) == set()
```

### Step 9: Assign n_src = value

```python
n_src = conn.shape[0]
```

**Verification:**
```python
assert n_src * 0.02 < conn.data.size < n_src * 0.1
```

### Step 10: Call assert_equal()

```python
assert_equal(conn[:src[0]['nuse'], :src[0]['nuse']].data.size, 0)
```

### Step 11: Call assert_equal()

```python
assert_equal(conn[-src[1]['nuse']:, -src[1]['nuse']:].data.size, 0)
```

### Step 12: Assign c = value

```python
c = (conn.T + conn) / 2.0 - conn
```

### Step 13: Call c.eliminate_zeros()

```python
c.eliminate_zeros()
```

### Step 14: Call assert_equal()

```python
assert_equal(c.data.size, 0)
```

### Step 15: Assign upper_right = unknown.toarray(...)

```python
upper_right = conn[:src[0]['nuse'], src[0]['nuse']:].toarray()
```

### Step 16: Call assert_equal()

```python
assert_equal(upper_right.sum(), conn.sum() // 2)
```

### Step 17: Assign good_labels = value

```python
good_labels = ['S_pericallosal', 'Unknown', 'G_and_S_cingul-Mid-Post', 'G_cuneus']
```

### Step 18: Assign has_neighbors = value

```python
has_neighbors = src[hi]['vertno'][np.where(np.any(upper_right, axis=1 - hi))[0]]
```

### Step 19: Assign labels = read_labels_from_annot(...)

```python
labels = read_labels_from_annot('sample', 'aparc.a2009s', hemi, subjects_dir=subjects_dir)
```

### Step 20: Assign use_labels = value

```python
use_labels = [label.name[:-3] for label in labels if np.isin(label.vertices, has_neighbors).any()]
```

**Verification:**
```python
assert set(use_labels) - set(good_labels) == set()
```


## Complete Example

```python
# Workflow
'Test spatial adjacency between hemispheres.'
conn = spatial_inter_hemi_adjacency(fname_src_3, 5e-06)
assert_equal(conn.data.size, 0)
conn = spatial_inter_hemi_adjacency(fname_src_3, 5000000.0)
assert_equal(conn.data.size, np.prod(conn.shape) // 2)
src = read_source_spaces(fname_src_3)
conn = spatial_inter_hemi_adjacency(src, 0.01)
conn = conn.tocsr()
n_src = conn.shape[0]
assert n_src * 0.02 < conn.data.size < n_src * 0.1
assert_equal(conn[:src[0]['nuse'], :src[0]['nuse']].data.size, 0)
assert_equal(conn[-src[1]['nuse']:, -src[1]['nuse']:].data.size, 0)
c = (conn.T + conn) / 2.0 - conn
c.eliminate_zeros()
assert_equal(c.data.size, 0)
upper_right = conn[:src[0]['nuse'], src[0]['nuse']:].toarray()
assert_equal(upper_right.sum(), conn.sum() // 2)
good_labels = ['S_pericallosal', 'Unknown', 'G_and_S_cingul-Mid-Post', 'G_cuneus']
for hi, hemi in enumerate(('lh', 'rh')):
    has_neighbors = src[hi]['vertno'][np.where(np.any(upper_right, axis=1 - hi))[0]]
    labels = read_labels_from_annot('sample', 'aparc.a2009s', hemi, subjects_dir=subjects_dir)
    use_labels = [label.name[:-3] for label in labels if np.isin(label.vertices, has_neighbors).any()]
    assert set(use_labels) - set(good_labels) == set()
```

## Next Steps


---

*Source: test_source_estimate.py:147 | Complexity: Advanced | Last updated: 2026-05-18*