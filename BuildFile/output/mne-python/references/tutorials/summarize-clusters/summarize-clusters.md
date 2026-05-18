# How To: Summarize Clusters

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test cluster summary stcs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne.fixes`
- `mne.stats`
- `mne.stats.cluster_level`
- `mne.utils`
- `sklearn.feature_extraction.image`
- `sklearn.feature_extraction.image`
- `sklearn.feature_extraction.image`

**Setup Required:**
```python
# Fixtures: kind
```

## Step-by-Step Guide

### Step 1: 'Test cluster summary stcs.'

```python
'Test cluster summary stcs.'
```

**Verification:**
```python
assert src_surf.kind == 'surface'
```

### Step 2: Assign src_surf = SourceSpaces(...)

```python
src_surf = SourceSpaces([dict(vertno=np.arange(10242), type='surf') for _ in range(2)])
```

**Verification:**
```python
assert src_vol.kind == 'volume'
```

### Step 3: Assign src_vol = SourceSpaces(...)

```python
src_vol = SourceSpaces([dict(vertno=np.arange(10), type='vol')])
```

**Verification:**
```python
assert kind == 'mixed'
```

### Step 4: Assign n_vertices = sum(...)

```python
n_vertices = sum((len(s['vertno']) for s in src))
```

**Verification:**
```python
assert len(src) == 1
```

### Step 5: Assign clu = value

```python
clu = (np.random.random([1, n_vertices]), [(np.array([0]), np.array([0, 2, 4]))], np.array([0.02, 0.1]), np.array([12, -14, 30]))
```

**Verification:**
```python
assert isinstance(stc_sum, klass)
```

### Step 6: Assign kwargs = dict(...)

```python
kwargs = dict()
```

**Verification:**
```python
assert stc_sum.data.shape[1] == 2
```

### Step 7: Assign stc_sum = summarize_clusters_stc(...)

```python
stc_sum = summarize_clusters_stc(clu, **kwargs)
```

**Verification:**
```python
assert isinstance(stc_sum, klass)
```

### Step 8: Assign unknown = 0.3

```python
clu[2][0] = 0.3
```

### Step 9: Assign src = src_surf

```python
src = src_surf
```

### Step 10: Assign klass = SourceEstimate

```python
klass = SourceEstimate
```

**Verification:**
```python
assert len(src) == 1
```

### Step 11: Assign unknown = value

```python
kwargs['vertices'] = [src[0]['vertno']]
```

### Step 12: Call summarize_clusters_stc()

```python
summarize_clusters_stc(clu, **kwargs)
```

### Step 13: Assign src = src_vol

```python
src = src_vol
```

### Step 14: Assign klass = VolSourceEstimate

```python
klass = VolSourceEstimate
```

**Verification:**
```python
assert kind == 'mixed'
```

### Step 15: Assign src = value

```python
src = src_surf + src_vol
```

### Step 16: Assign klass = MixedSourceEstimate

```python
klass = MixedSourceEstimate
```

### Step 17: Call summarize_clusters_stc()

```python
summarize_clusters_stc(clu)
```

### Step 18: Assign unknown = src

```python
kwargs['vertices'] = src
```


## Complete Example

```python
# Setup
# Fixtures: kind

# Workflow
'Test cluster summary stcs.'
src_surf = SourceSpaces([dict(vertno=np.arange(10242), type='surf') for _ in range(2)])
assert src_surf.kind == 'surface'
src_vol = SourceSpaces([dict(vertno=np.arange(10), type='vol')])
assert src_vol.kind == 'volume'
if kind == 'surface':
    src = src_surf
    klass = SourceEstimate
elif kind == 'volume':
    src = src_vol
    klass = VolSourceEstimate
else:
    assert kind == 'mixed'
    src = src_surf + src_vol
    klass = MixedSourceEstimate
n_vertices = sum((len(s['vertno']) for s in src))
clu = (np.random.random([1, n_vertices]), [(np.array([0]), np.array([0, 2, 4]))], np.array([0.02, 0.1]), np.array([12, -14, 30]))
kwargs = dict()
if kind == 'volume':
    with pytest.raises(ValueError, match='did not match'):
        summarize_clusters_stc(clu)
    assert len(src) == 1
    kwargs['vertices'] = [src[0]['vertno']]
elif kind == 'mixed':
    kwargs['vertices'] = src
stc_sum = summarize_clusters_stc(clu, **kwargs)
assert isinstance(stc_sum, klass)
assert stc_sum.data.shape[1] == 2
clu[2][0] = 0.3
with pytest.raises(RuntimeError, match='No significant'):
    summarize_clusters_stc(clu, **kwargs)
```

## Next Steps


---

*Source: test_cluster_level.py:729 | Complexity: Advanced | Last updated: 2026-05-18*