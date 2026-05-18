# How To: Add Sensors Scales

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test sensor_scales parameter.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `contextlib`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.lines`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.utils`
- `mne.viz`
- `mne.viz._brain`
- `mne.viz._brain.colormap`
- `mne.viz.utils`
- `mne.viz._brain`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: renderer_interactive_pyvistaqt, sensor_colors, sensor_scales, expectation
```

## Step-by-Step Guide

### Step 1: 'Test sensor_scales parameter.'

```python
'Test sensor_scales parameter.'
```

### Step 2: Assign kwargs = dict(...)

```python
kwargs = dict(subject=subject, subjects_dir=subjects_dir)
```

### Step 3: Assign hemi = 'lh'

```python
hemi = 'lh'
```

### Step 4: Assign surf = 'white'

```python
surf = 'white'
```

### Step 5: Assign cortex = 'low_contrast'

```python
cortex = 'low_contrast'
```

### Step 6: Assign title = 'test'

```python
title = 'test'
```

### Step 7: Assign size = value

```python
size = (300, 300)
```

### Step 8: Assign brain = Brain(...)

```python
brain = Brain(hemi=hemi, surf=surf, size=size, title=title, cortex=cortex, units='m', silhouette=dict(decimate=0.95), **kwargs)
```

### Step 9: Assign proj_info = create_info(...)

```python
proj_info = create_info([f'Ch{i}' for i in range(1, 7)], 1000, 'seeg')
```

### Step 10: Assign pos = value

```python
pos = np.array([[25.85, 9.04, -5.38], [33.56, 9.04, -5.63], [40.44, 9.04, -5.06], [46.75, 9.04, -6.78], [-30.08, 9.04, 28.23], [-32.95, 9.04, 37.99]]) / 1000
```

### Step 11: Call proj_info.set_montage()

```python
proj_info.set_montage(make_dig_montage(ch_pos=dict(zip(proj_info.ch_names, pos)), coord_frame='head'))
```

### Step 12: Call brain.close()

```python
brain.close()
```

### Step 13: Call brain.add_sensors()

```python
brain.add_sensors(proj_info, trans=fname_trans, sensor_colors=sensor_colors, sensor_scales=sensor_scales)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, sensor_colors, sensor_scales, expectation

# Workflow
'Test sensor_scales parameter.'
kwargs = dict(subject=subject, subjects_dir=subjects_dir)
hemi = 'lh'
surf = 'white'
cortex = 'low_contrast'
title = 'test'
size = (300, 300)
brain = Brain(hemi=hemi, surf=surf, size=size, title=title, cortex=cortex, units='m', silhouette=dict(decimate=0.95), **kwargs)
proj_info = create_info([f'Ch{i}' for i in range(1, 7)], 1000, 'seeg')
pos = np.array([[25.85, 9.04, -5.38], [33.56, 9.04, -5.63], [40.44, 9.04, -5.06], [46.75, 9.04, -6.78], [-30.08, 9.04, 28.23], [-32.95, 9.04, 37.99]]) / 1000
proj_info.set_montage(make_dig_montage(ch_pos=dict(zip(proj_info.ch_names, pos)), coord_frame='head'))
with expectation:
    brain.add_sensors(proj_info, trans=fname_trans, sensor_colors=sensor_colors, sensor_scales=sensor_scales)
brain.close()
```

## Next Steps


---

*Source: test_brain.py:635 | Complexity: Advanced | Last updated: 2026-05-18*