# How To: Plot Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of CTF evoked.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.collections`
- `matplotlib.colors`
- `mpl_toolkits.axes_grid1.parasite_axes`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.stats.parametric`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plotting of CTF evoked.'

```python
'Test plotting of CTF evoked.'
```

**Verification:**
```python
assert (np.linalg.norm(midpoints_before - midpoints_after) < 0.1).all()
```

### Step 2: Assign raw = mne.io.read_raw_ctf(...)

```python
raw = mne.io.read_raw_ctf(ctf_fname, preload=True)
```

### Step 3: Assign events = np.array(...)

```python
events = np.array([[200, 0, 1]])
```

### Step 4: Assign event_id = 1

```python
event_id = 1
```

### Step 5: Assign unknown = value

```python
tmin, tmax = (-0.1, 0.5)
```

### Step 6: Assign picks = value

```python
picks = mne.pick_types(raw.info, meg=True, stim=True, eog=True, ref_meg=True, exclude='bads')[::20]
```

### Step 7: Assign epochs = mne.Epochs(...)

```python
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, proj=True, picks=picks, preload=True, decim=10, verbose='error')
```

### Step 8: Assign evoked = epochs.average(...)

```python
evoked = epochs.average()
```

### Step 9: Call evoked.plot_joint()

```python
evoked.plot_joint(times=[0.1])
```

### Step 10: Call mne.viz.plot_compare_evokeds()

```python
mne.viz.plot_compare_evokeds([evoked, evoked])
```

### Step 11: Assign times = value

```python
times = [0.1, 0.2, 0.3]
```

### Step 12: Assign fig = plt.figure(...)

```python
fig = plt.figure()
```

### Step 13: Assign gs = gridspec.GridSpec(...)

```python
gs = gridspec.GridSpec(3, 7, hspace=0.5, top=0.8, figure=fig)
```

### Step 14: Assign topo_axes = value

```python
topo_axes = [fig.add_subplot(gs[0, idx * 2:(idx + 1) * 2]) for idx in range(len(times))]
```

### Step 15: Call topo_axes.append()

```python
topo_axes.append(fig.add_subplot(gs[0, -1]))
```

### Step 16: Assign ts_axis = fig.add_subplot(...)

```python
ts_axis = fig.add_subplot(gs[1:, 1:-1])
```

### Step 17: Assign midpoints_before = get_axes_midpoints(...)

```python
midpoints_before = get_axes_midpoints(topo_axes)
```

### Step 18: Call evoked.plot_joint()

```python
evoked.plot_joint(times=times, ts_args={'axes': ts_axis}, topomap_args={'axes': topo_axes}, title=None)
```

### Step 19: Assign midpoints_after = get_axes_midpoints(...)

```python
midpoints_after = get_axes_midpoints(topo_axes)
```

**Verification:**
```python
assert (np.linalg.norm(midpoints_before - midpoints_after) < 0.1).all()
```

### Step 20: Call evoked.plot_joint()

```python
evoked.plot_joint(times=[0.1], ts_args=dict(ylim=(-10, 10)))
```

### Step 21: Assign midpoints = list(...)

```python
midpoints = list()
```

### Step 22: Assign pos = ax.get_position(...)

```python
pos = ax.get_position()
```

### Step 23: Call midpoints.append()

```python
midpoints.append([pos.x0 + pos.width * 0.5, pos.y0 + pos.height * 0.5])
```


## Complete Example

```python
# Workflow
'Test plotting of CTF evoked.'
raw = mne.io.read_raw_ctf(ctf_fname, preload=True)
events = np.array([[200, 0, 1]])
event_id = 1
tmin, tmax = (-0.1, 0.5)
picks = mne.pick_types(raw.info, meg=True, stim=True, eog=True, ref_meg=True, exclude='bads')[::20]
epochs = mne.Epochs(raw, events, event_id, tmin, tmax, proj=True, picks=picks, preload=True, decim=10, verbose='error')
evoked = epochs.average()
evoked.plot_joint(times=[0.1])
with pytest.raises(TypeError, match='ylim must be an instance of dict or None'):
    evoked.plot_joint(times=[0.1], ts_args=dict(ylim=(-10, 10)))
mne.viz.plot_compare_evokeds([evoked, evoked])
times = [0.1, 0.2, 0.3]
fig = plt.figure()
gs = gridspec.GridSpec(3, 7, hspace=0.5, top=0.8, figure=fig)
topo_axes = [fig.add_subplot(gs[0, idx * 2:(idx + 1) * 2]) for idx in range(len(times))]
topo_axes.append(fig.add_subplot(gs[0, -1]))
ts_axis = fig.add_subplot(gs[1:, 1:-1])

def get_axes_midpoints(axes):
    midpoints = list()
    for ax in axes[:-1]:
        pos = ax.get_position()
        midpoints.append([pos.x0 + pos.width * 0.5, pos.y0 + pos.height * 0.5])
    return np.array(midpoints)
midpoints_before = get_axes_midpoints(topo_axes)
evoked.plot_joint(times=times, ts_args={'axes': ts_axis}, topomap_args={'axes': topo_axes}, title=None)
midpoints_after = get_axes_midpoints(topo_axes)
assert (np.linalg.norm(midpoints_before - midpoints_after) < 0.1).all()
```

## Next Steps


---

*Source: test_evoked.py:628 | Complexity: Advanced | Last updated: 2026-05-18*