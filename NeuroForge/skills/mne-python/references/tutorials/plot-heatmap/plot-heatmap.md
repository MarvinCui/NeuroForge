# How To: Plot Heatmap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_gaze.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `pytest`
- `mne`
- `mne._fiff.constants`

**Setup Required:**
```python
# Fixtures: eyetrack_raw, eyetrack_cal, axes, unit
```

## Step-by-Step Guide

### Step 1: 'Test plot_gaze.'

```python
'Test plot_gaze.'
```

**Verification:**
```python
assert img.T[width // 2, height // 2] == 1
```

### Step 2: Assign epochs = mne.make_fixed_length_epochs(...)

```python
epochs = mne.make_fixed_length_epochs(eyetrack_raw, duration=1.0)
```

### Step 3: Call epochs.load_data()

```python
epochs.load_data()
```

### Step 4: Assign unknown = value

```python
width, height = eyetrack_cal['screen_resolution']
```

### Step 5: Assign img = unknown.get_array(...)

```python
img = fig.axes[0].images[0].get_array()
```

**Verification:**
```python
assert img.T[width // 2, height // 2] == 1
```

### Step 6: Call mne.preprocessing.eyetracking.convert_units()

```python
mne.preprocessing.eyetracking.convert_units(epochs, eyetrack_cal, to='radians')
```

### Step 7: Assign axes = plt.subplot(...)

```python
axes = plt.subplot()
```

### Step 8: Call mne.viz.eyetracking.plot_gaze()

```python
mne.viz.eyetracking.plot_gaze(epochs)
```

### Step 9: Call mne.viz.eyetracking.plot_gaze()

```python
mne.viz.eyetracking.plot_gaze(epochs, width=width, height=height, calibration=eyetrack_cal)
```

### Step 10: Assign ep_bad = epochs.copy(...)

```python
ep_bad = epochs.copy()
```

### Step 11: Assign unknown = value

```python
ep_bad.info['chs'][0]['unit'] = FIFF.FIFF_UNIT_NONE
```

### Step 12: Call mne.viz.eyetracking.plot_gaze()

```python
mne.viz.eyetracking.plot_gaze(ep_bad, calibration=eyetrack_cal)
```

### Step 13: Assign fig = mne.viz.eyetracking.plot_gaze(...)

```python
fig = mne.viz.eyetracking.plot_gaze(epochs, width=width, height=height, axes=axes, cmap='Greys', sigma=None)
```

### Step 14: Call mne.viz.eyetracking.plot_gaze()

```python
mne.viz.eyetracking.plot_gaze(epochs, axes=axes, width=1, height=1)
```

### Step 15: Assign fig = mne.viz.eyetracking.plot_gaze(...)

```python
fig = mne.viz.eyetracking.plot_gaze(epochs, calibration=eyetrack_cal, axes=axes, cmap='Greys', sigma=None)
```


## Complete Example

```python
# Setup
# Fixtures: eyetrack_raw, eyetrack_cal, axes, unit

# Workflow
'Test plot_gaze.'
epochs = mne.make_fixed_length_epochs(eyetrack_raw, duration=1.0)
epochs.load_data()
width, height = eyetrack_cal['screen_resolution']
if unit == 'rad':
    mne.preprocessing.eyetracking.convert_units(epochs, eyetrack_cal, to='radians')
if axes:
    axes = plt.subplot()
with pytest.raises(ValueError, match='If no calibration is provided'):
    mne.viz.eyetracking.plot_gaze(epochs)
with pytest.raises(ValueError, match='If a calibration is provided'):
    mne.viz.eyetracking.plot_gaze(epochs, width=width, height=height, calibration=eyetrack_cal)
with pytest.raises(ValueError, match='Invalid unit'):
    ep_bad = epochs.copy()
    ep_bad.info['chs'][0]['unit'] = FIFF.FIFF_UNIT_NONE
    mne.viz.eyetracking.plot_gaze(ep_bad, calibration=eyetrack_cal)
if unit == 'rad':
    with pytest.raises(ValueError, match='If gaze data are in Radians'):
        mne.viz.eyetracking.plot_gaze(epochs, axes=axes, width=1, height=1)
if unit == 'px':
    fig = mne.viz.eyetracking.plot_gaze(epochs, width=width, height=height, axes=axes, cmap='Greys', sigma=None)
elif unit == 'rad':
    fig = mne.viz.eyetracking.plot_gaze(epochs, calibration=eyetrack_cal, axes=axes, cmap='Greys', sigma=None)
img = fig.axes[0].images[0].get_array()
assert img.T[width // 2, height // 2] == 1
```

## Next Steps


---

*Source: test_heatmap.py:13 | Complexity: Advanced | Last updated: 2026-05-18*