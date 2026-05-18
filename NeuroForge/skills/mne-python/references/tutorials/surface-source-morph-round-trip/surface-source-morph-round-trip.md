# How To: Surface Source Morph Round Trip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test round-trip morphing yields similar STCs.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: smooth, lower, upper, n_warn, dtype
```

## Step-by-Step Guide

### Step 1: 'Test round-trip morphing yields similar STCs.'

```python
'Test round-trip morphing yields similar STCs.'
```

**Verification:**
```python
assert_array_equal(stc.data.real, 0.0)
```

### Step 2: Assign kwargs = dict(...)

```python
kwargs = dict(smooth=smooth, warn=True, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert len(w) == n_warn
```

### Step 3: Assign stc = mne.read_source_estimate(...)

```python
stc = mne.read_source_estimate(fname_smorph)
```

**Verification:**
```python
assert morph.morph_mat.shape == (20484, len(stc.data))
```

### Step 4: Assign w = value

```python
w = [ww for ww in w if 'vertices not included' in str(ww.message)]
```

**Verification:**
```python
assert morph_back.morph_mat.shape == (len(stc.data), 20484)
```

### Step 5: Assign stc_fs = morph.apply(...)

```python
stc_fs = morph.apply(stc)
```

**Verification:**
```python
assert lower <= corr <= upper
```

### Step 6: Assign morph_back = compute_source_morph(...)

```python
morph_back = compute_source_morph(stc_fs, 'fsaverage', 'sample', spacing=stc.vertices, **kwargs)
```

**Verification:**
```python
assert_power_preserved(stc, stc_back)
```

### Step 7: Assign stc_back = morph_back.apply(...)

```python
stc_back = morph_back.apply(stc_fs)
```

### Step 8: Assign corr = value

```python
corr = np.corrcoef(stc.data.ravel(), stc_back.data.ravel())[0, 1]
```

**Verification:**
```python
assert lower <= corr <= upper
```

### Step 9: Call assert_power_preserved()

```python
assert_power_preserved(stc, stc_back)
```

### Step 10: Assign stc.data = value

```python
stc.data = 1j * stc.data
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(stc.data.real, 0.0)
```

### Step 12: Assign morph = compute_source_morph(...)

```python
morph = compute_source_morph(stc, 'sample', 'fsaverage', **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: smooth, lower, upper, n_warn, dtype

# Workflow
'Test round-trip morphing yields similar STCs.'
kwargs = dict(smooth=smooth, warn=True, subjects_dir=subjects_dir)
stc = mne.read_source_estimate(fname_smorph)
if dtype is complex:
    stc.data = 1j * stc.data
    assert_array_equal(stc.data.real, 0.0)
with _record_warnings() as w:
    morph = compute_source_morph(stc, 'sample', 'fsaverage', **kwargs)
w = [ww for ww in w if 'vertices not included' in str(ww.message)]
assert len(w) == n_warn
assert morph.morph_mat.shape == (20484, len(stc.data))
stc_fs = morph.apply(stc)
morph_back = compute_source_morph(stc_fs, 'fsaverage', 'sample', spacing=stc.vertices, **kwargs)
assert morph_back.morph_mat.shape == (len(stc.data), 20484)
stc_back = morph_back.apply(stc_fs)
corr = np.corrcoef(stc.data.ravel(), stc_back.data.ravel())[0, 1]
assert lower <= corr <= upper
assert_power_preserved(stc, stc_back)
```

## Next Steps


---

*Source: test_morph.py:241 | Complexity: Advanced | Last updated: 2026-05-18*