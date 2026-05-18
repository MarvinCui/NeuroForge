# How To: Make Montage Volume

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test making a montage image based on intracranial electrodes.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.preprocessing.ieeg`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: 'Test making a montage image based on intracranial electrodes.'

```python
'Test making a montage image based on intracranial electrodes.'
```

**Verification:**
```python
assert np.linalg.norm(np.array(np.where(elec_image_data == i + 1)).mean(axis=1) - ch_coords_vox[i]) < 0.5
```

### Step 2: Assign nib = pytest.importorskip(...)

```python
nib = pytest.importorskip('nibabel')
```

### Step 3: Call pytest.importorskip()

```python
pytest.importorskip('dipy')
```

### Step 4: Assign subject_brain = nib.load(...)

```python
subject_brain = nib.load(subjects_dir / 'sample' / 'mri' / 'brain.mgz')
```

### Step 5: Assign ch_coords = np.array(...)

```python
ch_coords = np.array([[-8.7040273, 17.99938754, 10.29604017], [-14.03007764, 19.69978401, 12.07236939], [-21.1130506, 21.98310911, 13.25658887]])
```

### Step 6: Assign ch_pos = dict(...)

```python
ch_pos = dict(zip(['1', '2', '3'], ch_coords / 1000))
```

### Step 7: Assign unknown = get_mni_fiducials(...)

```python
lpa, nasion, rpa = get_mni_fiducials('sample', subjects_dir)
```

### Step 8: Assign montage = make_dig_montage(...)

```python
montage = make_dig_montage(ch_pos, lpa=lpa['r'], nasion=nasion['r'], rpa=rpa['r'], coord_frame='mri')
```

### Step 9: Assign CT_data = np.zeros(...)

```python
CT_data = np.zeros(subject_brain.shape)
```

### Step 10: Assign ch_coords_vox = apply_trans(...)

```python
ch_coords_vox = apply_trans(np.linalg.inv(subject_brain.header.get_vox2ras_tkr()), ch_coords)
```

### Step 11: Assign CT = nib.Nifti1Image(...)

```python
CT = nib.Nifti1Image(CT_data, subject_brain.affine)
```

### Step 12: Assign elec_image = make_montage_volume(...)

```python
elec_image = make_montage_volume(montage, CT, thresh=0.25)
```

### Step 13: Assign elec_image_data = np.array(...)

```python
elec_image_data = np.array(elec_image.dataobj)
```

### Step 14: Assign bad_montage = montage.copy(...)

```python
bad_montage = montage.copy()
```

### Step 15: Assign unknown = 500

```python
CT_data[x - 1:x + 2, y - 1:y + 2, z - 1:z + 2] = 500
```

### Step 16: Assign unknown = 1000

```python
CT_data[x, y, z] = 1000
```

**Verification:**
```python
assert np.linalg.norm(np.array(np.where(elec_image_data == i + 1)).mean(axis=1) - ch_coords_vox[i]) < 0.5
```

### Step 17: Call make_montage_volume()

```python
make_montage_volume(montage, CT, thresh=11.0)
```

### Step 18: Assign unknown = 99

```python
d['coord_frame'] = 99
```

### Step 19: Call make_montage_volume()

```python
make_montage_volume(bad_montage, CT)
```


## Complete Example

```python
# Workflow
'Test making a montage image based on intracranial electrodes.'
nib = pytest.importorskip('nibabel')
pytest.importorskip('dipy')
subject_brain = nib.load(subjects_dir / 'sample' / 'mri' / 'brain.mgz')
ch_coords = np.array([[-8.7040273, 17.99938754, 10.29604017], [-14.03007764, 19.69978401, 12.07236939], [-21.1130506, 21.98310911, 13.25658887]])
ch_pos = dict(zip(['1', '2', '3'], ch_coords / 1000))
lpa, nasion, rpa = get_mni_fiducials('sample', subjects_dir)
montage = make_dig_montage(ch_pos, lpa=lpa['r'], nasion=nasion['r'], rpa=rpa['r'], coord_frame='mri')
CT_data = np.zeros(subject_brain.shape)
ch_coords_vox = apply_trans(np.linalg.inv(subject_brain.header.get_vox2ras_tkr()), ch_coords)
for x, y, z in ch_coords_vox.round().astype(int):
    CT_data[x - 1:x + 2, y - 1:y + 2, z - 1:z + 2] = 500
    CT_data[x, y, z] = 1000
CT = nib.Nifti1Image(CT_data, subject_brain.affine)
elec_image = make_montage_volume(montage, CT, thresh=0.25)
elec_image_data = np.array(elec_image.dataobj)
for i in range(len(montage.ch_names)):
    assert np.linalg.norm(np.array(np.where(elec_image_data == i + 1)).mean(axis=1) - ch_coords_vox[i]) < 0.5
with pytest.raises(ValueError, match='`thresh` must be between 0 and 1'):
    make_montage_volume(montage, CT, thresh=11.0)
bad_montage = montage.copy()
for d in bad_montage.dig:
    d['coord_frame'] = 99
with pytest.raises(RuntimeError, match='Coordinate frame not supported'):
    make_montage_volume(bad_montage, CT)
```

## Next Steps


---

*Source: test_volume.py:76 | Complexity: Advanced | Last updated: 2026-05-18*