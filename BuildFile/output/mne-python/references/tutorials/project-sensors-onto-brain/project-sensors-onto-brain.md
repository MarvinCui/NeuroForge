# How To: Project Sensors Onto Brain

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test projecting sensors onto the brain surface.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.preprocessing.ieeg`
- `mne.preprocessing.ieeg._projection`
- `mne.transforms`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test projecting sensors onto the brain surface.'

```python
'Test projecting sensors onto the brain surface.'
```

**Verification:**
```python
assert montage is not None
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert_allclose(ch_pos[ch], test_loc, atol=0.01)
```

### Step 3: Assign raw = mne.io.read_raw_fif(...)

```python
raw = mne.io.read_raw_fif(fname_raw)
```

### Step 4: Assign trans = value

```python
trans = _get_trans(fname_trans)[0]
```

### Step 5: Assign brain_surf_fname = value

```python
brain_surf_fname = tmp_path / 'sample' / 'bem' / 'brain.surf'
```

### Step 6: Call raw.pick()

```python
raw.pick('eeg')
```

### Step 7: Call raw.load_data()

```python
raw.load_data()
```

### Step 8: Call raw.set_eeg_reference()

```python
raw.set_eeg_reference([])
```

### Step 9: Call raw.set_channel_types()

```python
raw.set_channel_types({ch: 'ecog' for ch in raw.ch_names})
```

### Step 10: Assign pos = np.zeros(...)

```python
pos = np.zeros((49, 3))
```

### Step 11: Assign unknown = value

```python
pos[:, :2] = np.array(np.meshgrid(np.linspace(0, 0.02, 7), np.linspace(0, 0.02, 7))).reshape(2, -1).T
```

### Step 12: Assign unknown = 0.12

```python
pos[:, 2] = 0.12
```

### Step 13: Call raw.drop_channels()

```python
raw.drop_channels(raw.ch_names[49:])
```

### Step 14: Call raw.set_montage()

```python
raw.set_montage(mne.channels.make_dig_montage(ch_pos=dict(zip(raw.ch_names[:49], pos)), coord_frame='head'))
```

### Step 15: Assign raw.info = project_sensors_onto_brain(...)

```python
raw.info = project_sensors_onto_brain(raw.info, trans, 'sample', subjects_dir=tmp_path)
```

### Step 16: Assign test_locs = value

```python
test_locs = [[0.00149, -0.001588, 0.133029], [0.004302, 0.001959, 0.133922], [0.008602, 0.00116, 0.133723]]
```

### Step 17: Assign montage = raw.get_montage(...)

```python
montage = raw.get_montage()
```

**Verification:**
```python
assert montage is not None
```

### Step 18: Assign ch_pos = value

```python
ch_pos = montage.get_positions()['ch_pos']
```

### Step 19: Call project_sensors_onto_brain()

```python
project_sensors_onto_brain(raw.info, trans, 'sample', subjects_dir=tmp_path)
```

### Step 20: Call os.makedirs()

```python
os.makedirs(brain_surf_fname.parent)
```

### Step 21: Call copyfile()

```python
copyfile(subjects_dir / 'sample' / 'bem' / 'inner_skull.surf', brain_surf_fname)
```

### Step 22: Call assert_allclose()

```python
assert_allclose(ch_pos[ch], test_loc, atol=0.01)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test projecting sensors onto the brain surface.'
pytest.importorskip('nibabel')
raw = mne.io.read_raw_fif(fname_raw)
trans = _get_trans(fname_trans)[0]
with pytest.raises(RuntimeError, match='requires generating a BEM'):
    project_sensors_onto_brain(raw.info, trans, 'sample', subjects_dir=tmp_path)
brain_surf_fname = tmp_path / 'sample' / 'bem' / 'brain.surf'
if not brain_surf_fname.parent.is_dir():
    os.makedirs(brain_surf_fname.parent)
if not brain_surf_fname.is_file():
    copyfile(subjects_dir / 'sample' / 'bem' / 'inner_skull.surf', brain_surf_fname)
raw.pick('eeg')
raw.load_data()
raw.set_eeg_reference([])
raw.set_channel_types({ch: 'ecog' for ch in raw.ch_names})
pos = np.zeros((49, 3))
pos[:, :2] = np.array(np.meshgrid(np.linspace(0, 0.02, 7), np.linspace(0, 0.02, 7))).reshape(2, -1).T
pos[:, 2] = 0.12
raw.drop_channels(raw.ch_names[49:])
raw.set_montage(mne.channels.make_dig_montage(ch_pos=dict(zip(raw.ch_names[:49], pos)), coord_frame='head'))
raw.info = project_sensors_onto_brain(raw.info, trans, 'sample', subjects_dir=tmp_path)
test_locs = [[0.00149, -0.001588, 0.133029], [0.004302, 0.001959, 0.133922], [0.008602, 0.00116, 0.133723]]
montage = raw.get_montage()
assert montage is not None
ch_pos = montage.get_positions()['ch_pos']
for ch, test_loc in zip(raw.ch_names[:3], test_locs):
    assert_allclose(ch_pos[ch], test_loc, atol=0.01)
```

## Next Steps


---

*Source: test_projection.py:27 | Complexity: Advanced | Last updated: 2026-05-18*