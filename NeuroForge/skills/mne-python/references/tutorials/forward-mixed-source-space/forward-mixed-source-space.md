# How To: Forward Mixed Source Space

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test making the forward solution for a mixed source space.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test making the forward solution for a mixed source space.'

```python
'Test making the forward solution for a mixed source space.'
```

**Verification:**
```python
assert repr(fwd)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert (coord_frames == FIFF.FIFFV_COORD_HEAD).all()
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 4: Assign surf = read_source_spaces(...)

```python
surf = read_source_spaces(fname_src)
```

### Step 5: Assign label_names = get_volume_labels_from_aseg(...)

```python
label_names = get_volume_labels_from_aseg(fname_aseg)
```

### Step 6: Assign vol_labels = rng.choice(...)

```python
vol_labels = rng.choice(label_names, 2)
```

### Step 7: Assign vol2 = setup_volume_source_space(...)

```python
vol2 = setup_volume_source_space('sample', pos=20.0, mri=fname_aseg, volume_label=vol_labels[1], add_interpolator=False)
```

### Step 8: Assign src = value

```python
src = surf + vol1 + vol2
```

### Step 9: Assign fwd = make_forward_solution(...)

```python
fwd = make_forward_solution(fname_raw, fname_trans, src, fname_bem)
```

**Verification:**
```python
assert repr(fwd)
```

### Step 10: Assign src_from_fwd = value

```python
src_from_fwd = fwd['src']
```

### Step 11: Assign coord_frames = np.array(...)

```python
coord_frames = np.array([s['coord_frame'] for s in src_from_fwd])
```

**Verification:**
```python
assert (coord_frames == FIFF.FIFFV_COORD_HEAD).all()
```

### Step 12: Assign fname_img = value

```python
fname_img = tmp_path / 'temp-image.mgz'
```

### Step 13: Assign vox_mri_t = value

```python
vox_mri_t = vol1[0]['vox_mri_t']
```

### Step 14: Assign vol1 = setup_volume_source_space(...)

```python
vol1 = setup_volume_source_space('sample', pos=20.0, mri=fname_aseg, volume_label=vol_labels[0], add_interpolator=False)
```

### Step 15: Call src_from_fwd.export_volume()

```python
src_from_fwd.export_volume(fname_img, mri_resolution=True, trans=None)
```

### Step 16: Call src_from_fwd.export_volume()

```python
src_from_fwd.export_volume(fname_img, mri_resolution=True, trans=vox_mri_t)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test making the forward solution for a mixed source space.'
pytest.importorskip('nibabel')
rng = np.random.RandomState(0)
surf = read_source_spaces(fname_src)
label_names = get_volume_labels_from_aseg(fname_aseg)
vol_labels = rng.choice(label_names, 2)
with pytest.warns(RuntimeWarning, match='Found no usable.*CC_Mid_Ant.*'):
    vol1 = setup_volume_source_space('sample', pos=20.0, mri=fname_aseg, volume_label=vol_labels[0], add_interpolator=False)
vol2 = setup_volume_source_space('sample', pos=20.0, mri=fname_aseg, volume_label=vol_labels[1], add_interpolator=False)
src = surf + vol1 + vol2
fwd = make_forward_solution(fname_raw, fname_trans, src, fname_bem)
assert repr(fwd)
src_from_fwd = fwd['src']
coord_frames = np.array([s['coord_frame'] for s in src_from_fwd])
assert (coord_frames == FIFF.FIFFV_COORD_HEAD).all()
fname_img = tmp_path / 'temp-image.mgz'
with pytest.raises(ValueError, match='trans containing mri to head'):
    src_from_fwd.export_volume(fname_img, mri_resolution=True, trans=None)
vox_mri_t = vol1[0]['vox_mri_t']
with pytest.raises(ValueError, match='head<->mri, got mri_voxel->mri'):
    src_from_fwd.export_volume(fname_img, mri_resolution=True, trans=vox_mri_t)
```

## Next Steps


---

*Source: test_make_forward.py:654 | Complexity: Advanced | Last updated: 2026-05-18*