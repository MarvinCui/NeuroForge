# How To: Brain Linkviewer

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test _LinkViewer primitives.

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
# Fixtures: renderer_interactive_pyvistaqt, brain_gc
```

## Step-by-Step Guide

### Step 1: 'Test _LinkViewer primitives.'

```python
'Test _LinkViewer primitives.'
```

### Step 2: Assign brain1 = _create_testing_brain(...)

```python
brain1 = _create_testing_brain(hemi='lh', show_traces=False)
```

### Step 3: Assign brain2 = _create_testing_brain(...)

```python
brain2 = _create_testing_brain(hemi='lh', show_traces='separate')
```

### Step 4: Assign brain1._times = value

```python
brain1._times = brain1._times * 2
```

### Step 5: Call brain1.close()

```python
brain1.close()
```

### Step 6: Assign brain_data = _create_testing_brain(...)

```python
brain_data = _create_testing_brain(hemi='split', show_traces='vertex')
```

### Step 7: Assign link_viewer = _LinkViewer(...)

```python
link_viewer = _LinkViewer([brain2, brain_data], time=True, camera=True, colorbar=True, picking=True)
```

### Step 8: Call link_viewer.leader.set_time()

```python
link_viewer.leader.set_time(1)
```

### Step 9: Call link_viewer.leader.set_time_point()

```python
link_viewer.leader.set_time_point(0)
```

### Step 10: Call link_viewer.leader.update_lut()

```python
link_viewer.leader.update_lut(fmin=0, fmid=0.5, fmax=1)
```

### Step 11: Call link_viewer.leader.set_playback_speed()

```python
link_viewer.leader.set_playback_speed(0.1)
```

### Step 12: Call link_viewer.leader.toggle_playback()

```python
link_viewer.leader.toggle_playback()
```

### Step 13: Call ui_events.publish()

```python
ui_events.publish(link_viewer.leader, ui_events.TimeChange(time=0))
```

### Step 14: Call brain2.close()

```python
brain2.close()
```

### Step 15: Call brain_data.close()

```python
brain_data.close()
```

### Step 16: Call _LinkViewer()

```python
_LinkViewer([brain1, brain2], time=True, camera=False, colorbar=False, picking=False)
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, brain_gc

# Workflow
'Test _LinkViewer primitives.'
brain1 = _create_testing_brain(hemi='lh', show_traces=False)
brain2 = _create_testing_brain(hemi='lh', show_traces='separate')
brain1._times = brain1._times * 2
with pytest.warns(RuntimeWarning, match='linking time'):
    _LinkViewer([brain1, brain2], time=True, camera=False, colorbar=False, picking=False)
brain1.close()
brain_data = _create_testing_brain(hemi='split', show_traces='vertex')
link_viewer = _LinkViewer([brain2, brain_data], time=True, camera=True, colorbar=True, picking=True)
link_viewer.leader.set_time(1)
link_viewer.leader.set_time_point(0)
link_viewer.leader.update_lut(fmin=0, fmid=0.5, fmax=1)
link_viewer.leader.set_playback_speed(0.1)
link_viewer.leader.toggle_playback()
ui_events.publish(link_viewer.leader, ui_events.TimeChange(time=0))
brain2.close()
brain_data.close()
```

## Next Steps


---

*Source: test_brain.py:1279 | Complexity: Advanced | Last updated: 2026-05-18*