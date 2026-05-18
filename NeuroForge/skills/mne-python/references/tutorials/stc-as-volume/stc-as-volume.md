# How To: Stc As Volume

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test previous volume source estimate morph.

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

### Step 1: 'Test previous volume source estimate morph.'

```python
'Test previous volume source estimate morph.'
```

**Verification:**
```python
assert isinstance(img, nib.Nifti1Image)
```

### Step 2: Assign nib = pytest.importorskip(...)

```python
nib = pytest.importorskip('nibabel')
```

**Verification:**
```python
assert img.header.get_zooms()[:3] == t1_img.header.get_zooms()[:3]
```

### Step 3: Assign inverse_operator_vol = read_inverse_operator(...)

```python
inverse_operator_vol = read_inverse_operator(fname_inv_vol)
```

**Verification:**
```python
assert isinstance(img, nib.Nifti1Image)
```

### Step 4: Assign stc_vol = read_source_estimate(...)

```python
stc_vol = read_source_estimate(fname_vol, 'sample')
```

**Verification:**
```python
assert img.shape[:3] == inverse_operator_vol['src'][0]['shape'][:3]
```

### Step 5: Assign img = stc_vol.as_volume(...)

```python
img = stc_vol.as_volume(inverse_operator_vol['src'], mri_resolution=True, dest='42')
```

### Step 6: Assign t1_img = nib.load(...)

```python
t1_img = nib.load(fname_t1)
```

**Verification:**
```python
assert isinstance(img, nib.Nifti1Image)
```

### Step 7: Assign img = stc_vol.as_volume(...)

```python
img = stc_vol.as_volume(inverse_operator_vol['src'], mri_resolution=False)
```

**Verification:**
```python
assert isinstance(img, nib.Nifti1Image)
```

### Step 8: Call stc_vol.as_volume()

```python
stc_vol.as_volume(inverse_operator_vol['src'], format='42')
```


## Complete Example

```python
# Workflow
'Test previous volume source estimate morph.'
nib = pytest.importorskip('nibabel')
inverse_operator_vol = read_inverse_operator(fname_inv_vol)
stc_vol = read_source_estimate(fname_vol, 'sample')
img = stc_vol.as_volume(inverse_operator_vol['src'], mri_resolution=True, dest='42')
t1_img = nib.load(fname_t1)
assert isinstance(img, nib.Nifti1Image)
assert img.header.get_zooms()[:3] == t1_img.header.get_zooms()[:3]
img = stc_vol.as_volume(inverse_operator_vol['src'], mri_resolution=False)
assert isinstance(img, nib.Nifti1Image)
assert img.shape[:3] == inverse_operator_vol['src'][0]['shape'][:3]
with pytest.raises(ValueError, match='Invalid value.*output.*'):
    stc_vol.as_volume(inverse_operator_vol['src'], format='42')
```

## Next Steps


---

*Source: test_source_estimate.py:281 | Complexity: Advanced | Last updated: 2026-05-18*