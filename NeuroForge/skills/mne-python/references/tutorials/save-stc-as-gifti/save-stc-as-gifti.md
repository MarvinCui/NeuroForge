# How To: Save Stc As Gifti

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Save the stc as a GIFTI file and export.

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

### Step 1: 'Save the stc as a GIFTI file and export.'

```python
'Save the stc as a GIFTI file and export.'
```

**Verification:**
```python
assert isinstance(src, SourceSpaces)
```

### Step 2: Assign nib = pytest.importorskip(...)

```python
nib = pytest.importorskip('nibabel')
```

**Verification:**
```python
assert isinstance(stc, SourceEstimate)
```

### Step 3: Assign surfpath_src = value

```python
surfpath_src = bem_path / 'sample-oct-6-src.fif'
```

**Verification:**
```python
assert isinstance(img_lh, nib.gifti.gifti.GiftiImage)
```

### Step 4: Assign surfpath_stc = value

```python
surfpath_stc = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg'
```

**Verification:**
```python
assert isinstance(img_rh, nib.gifti.gifti.GiftiImage)
```

### Step 5: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(surfpath_src)
```

**Verification:**
```python
assert isinstance(img_timelh, nib.gifti.gifti.GiftiImage)
```

### Step 6: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(surfpath_stc)
```

**Verification:**
```python
assert isinstance(img_timerh, nib.gifti.gifti.GiftiImage)
```

### Step 7: Assign surf_fname = value

```python
surf_fname = tmp_path / 'stc_write'
```

### Step 8: Call stc.save_as_surface()

```python
stc.save_as_surface(surf_fname, src)
```

### Step 9: Assign img_lh = nib.load(...)

```python
img_lh = nib.load(f'{surf_fname}-lh.gii')
```

### Step 10: Assign img_rh = nib.load(...)

```python
img_rh = nib.load(f'{surf_fname}-rh.gii')
```

**Verification:**
```python
assert isinstance(img_lh, nib.gifti.gifti.GiftiImage)
```

### Step 11: Assign img_timelh = nib.load(...)

```python
img_timelh = nib.load(f'{surf_fname}-lh.time.gii')
```

### Step 12: Assign img_timerh = nib.load(...)

```python
img_timerh = nib.load(f'{surf_fname}-rh.time.gii')
```

**Verification:**
```python
assert isinstance(img_timelh, nib.gifti.gifti.GiftiImage)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Save the stc as a GIFTI file and export.'
nib = pytest.importorskip('nibabel')
surfpath_src = bem_path / 'sample-oct-6-src.fif'
surfpath_stc = data_path / 'MEG' / 'sample' / 'sample_audvis_trunc-meg'
src = read_source_spaces(surfpath_src)
stc = read_source_estimate(surfpath_stc)
assert isinstance(src, SourceSpaces)
assert isinstance(stc, SourceEstimate)
surf_fname = tmp_path / 'stc_write'
stc.save_as_surface(surf_fname, src)
img_lh = nib.load(f'{surf_fname}-lh.gii')
img_rh = nib.load(f'{surf_fname}-rh.gii')
assert isinstance(img_lh, nib.gifti.gifti.GiftiImage)
assert isinstance(img_rh, nib.gifti.gifti.GiftiImage)
img_timelh = nib.load(f'{surf_fname}-lh.time.gii')
img_timerh = nib.load(f'{surf_fname}-rh.time.gii')
assert isinstance(img_timelh, nib.gifti.gifti.GiftiImage)
assert isinstance(img_timerh, nib.gifti.gifti.GiftiImage)
```

## Next Steps


---

*Source: test_source_estimate.py:253 | Complexity: Advanced | Last updated: 2026-05-18*