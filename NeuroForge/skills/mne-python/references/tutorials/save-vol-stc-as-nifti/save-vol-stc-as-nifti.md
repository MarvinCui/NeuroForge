# How To: Save Vol Stc As Nifti

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Save the stc as a nifti file and export.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Save the stc as a nifti file and export.'

```python
'Save the stc as a nifti file and export.'
```

**Verification:**
```python
assert isinstance(stc, VolSourceEstimate)
```

### Step 2: Assign nib = pytest.importorskip(...)

```python
nib = pytest.importorskip('nibabel')
```

**Verification:**
```python
assert img.shape == src[0]['shape'] + (len(stc.times),)
```

### Step 3: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(fname_vsrc)
```

**Verification:**
```python
assert img.shape == t1_img.shape + (len(stc.times),)
```

### Step 4: Assign vol_fname = value

```python
vol_fname = tmp_path / 'stc.nii.gz'
```

**Verification:**
```python
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
```

### Step 5: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(fname_vol, 'sample')
```

**Verification:**
```python
assert img.shape == t1_img.shape + (len(stc.times),)
```

### Step 6: Call stc.save_as_volume()

```python
stc.save_as_volume(vol_fname, src, dest='surf', mri_resolution=False)
```

**Verification:**
```python
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
```

### Step 7: Call stc.save_as_volume()

```python
stc.save_as_volume(vol_fname, src, dest='mri', mri_resolution=True, overwrite=True)
```

**Verification:**
```python
assert img.shape == src[0]['shape'] + (len(stc.times),)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
```

### Step 9: Assign img = stc.as_volume(...)

```python
img = stc.as_volume(src, dest='mri', mri_resolution=True)
```

**Verification:**
```python
assert img.shape == t1_img.shape + (len(stc.times),)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
```

### Step 11: Assign src = SourceSpaces(...)

```python
src = SourceSpaces([src[0], src[0]])
```

### Step 12: Assign stc = VolSourceEstimate(...)

```python
stc = VolSourceEstimate(np.r_[stc.data, stc.data], [stc.vertices[0], stc.vertices[0]], tmin=stc.tmin, tstep=stc.tstep, subject='sample')
```

### Step 13: Assign img = stc.as_volume(...)

```python
img = stc.as_volume(src, dest='mri', mri_resolution=False)
```

**Verification:**
```python
assert img.shape == src[0]['shape'] + (len(stc.times),)
```

### Step 14: Assign img = nib.load(...)

```python
img = nib.load(str(vol_fname))
```

### Step 15: Assign t1_img = nib.load(...)

```python
t1_img = nib.load(fname_t1)
```

### Step 16: Assign img = nib.load(...)

```python
img = nib.load(str(vol_fname))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Save the stc as a nifti file and export.'
nib = pytest.importorskip('nibabel')
src = read_source_spaces(fname_vsrc)
vol_fname = tmp_path / 'stc.nii.gz'
stc = read_source_estimate(fname_vol, 'sample')
assert isinstance(stc, VolSourceEstimate)
stc.save_as_volume(vol_fname, src, dest='surf', mri_resolution=False)
with _record_warnings():
    img = nib.load(str(vol_fname))
assert img.shape == src[0]['shape'] + (len(stc.times),)
with _record_warnings():
    t1_img = nib.load(fname_t1)
stc.save_as_volume(vol_fname, src, dest='mri', mri_resolution=True, overwrite=True)
with _record_warnings():
    img = nib.load(str(vol_fname))
assert img.shape == t1_img.shape + (len(stc.times),)
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
img = stc.as_volume(src, dest='mri', mri_resolution=True)
assert img.shape == t1_img.shape + (len(stc.times),)
assert_allclose(img.affine, t1_img.affine, atol=1e-05)
src = SourceSpaces([src[0], src[0]])
stc = VolSourceEstimate(np.r_[stc.data, stc.data], [stc.vertices[0], stc.vertices[0]], tmin=stc.tmin, tstep=stc.tstep, subject='sample')
img = stc.as_volume(src, dest='mri', mri_resolution=False)
assert img.shape == src[0]['shape'] + (len(stc.times),)
```

## Next Steps


---

*Source: test_source_estimate.py:305 | Complexity: Advanced | Last updated: 2026-05-18*