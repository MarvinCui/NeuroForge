# How To: Surface Source Morph Shortcut

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that our shortcut for smooth=0 works.

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

### Step 1: 'Test that our shortcut for smooth=0 works.'

```python
'Test that our shortcut for smooth=0 works.'
```

**Verification:**
```python
assert_allclose(stc_back.data, stc.data, rtol=0.0001)
```

### Step 2: Assign stc = mne.read_source_estimate(...)

```python
stc = mne.read_source_estimate(fname_smorph)
```

**Verification:**
```python
assert abs_sum < 0.0001
```

### Step 3: Assign morph_identity = compute_source_morph(...)

```python
morph_identity = compute_source_morph(stc, 'sample', 'sample', spacing=stc.vertices, smooth=0, subjects_dir=subjects_dir)
```

### Step 4: Assign stc_back = morph_identity.apply(...)

```python
stc_back = morph_identity.apply(stc)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(stc_back.data, stc.data, rtol=0.0001)
```

### Step 6: Assign abs_sum = value

```python
abs_sum = morph_identity.morph_mat - speye(len(stc.data), format='csc')
```

### Step 7: Assign abs_sum = np.abs.sum(...)

```python
abs_sum = np.abs(abs_sum.data).sum()
```

**Verification:**
```python
assert abs_sum < 0.0001
```


## Complete Example

```python
# Workflow
'Test that our shortcut for smooth=0 works.'
stc = mne.read_source_estimate(fname_smorph)
morph_identity = compute_source_morph(stc, 'sample', 'sample', spacing=stc.vertices, smooth=0, subjects_dir=subjects_dir)
stc_back = morph_identity.apply(stc)
assert_allclose(stc_back.data, stc.data, rtol=0.0001)
abs_sum = morph_identity.morph_mat - speye(len(stc.data), format='csc')
abs_sum = np.abs(abs_sum.data).sum()
assert abs_sum < 0.0001
```

## Next Steps


---

*Source: test_morph.py:266 | Complexity: Intermediate | Last updated: 2026-05-18*