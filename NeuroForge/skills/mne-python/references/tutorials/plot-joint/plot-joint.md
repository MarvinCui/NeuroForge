# How To: Plot Joint

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test joint plot.

## Prerequisites

**Required Modules:**
- `collections`
- `pathlib`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.viz`
- `mne.viz.evoked`
- `mne.viz.topo`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test joint plot.'

```python
'Test joint plot.'
```

**Verification:**
```python
assert len(evoked.info['projs']) == 0
```

### Step 2: Assign evoked = _get_epochs.average(...)

```python
evoked = _get_epochs().average()
```

**Verification:**
```python
assert len(evoked.info['projs']) == 1
```

### Step 3: Call evoked.plot_joint()

```python
evoked.plot_joint(ts_args=dict(time_unit='s'), topomap_args=dict(time_unit='s'))
```

### Step 4: Call evoked.plot_joint()

```python
evoked.plot_joint(title='test', topomap_args=dict(contours=0, res=8, time_unit='ms'), ts_args=dict(spatial_colors=True, zorder=return_inds, time_unit='s'))
```

### Step 5: Assign axes = unknown.flatten.tolist(...)

```python
axes = plt.subplots(nrows=3)[-1].flatten().tolist()
```

### Step 6: Call evoked.plot_joint()

```python
evoked.plot_joint(times=[0], picks=[6, 7, 8], ts_args=dict(axes=axes[0]), topomap_args={'axes': axes[1:], 'time_unit': 's'})
```

### Step 7: Call plt.close()

```python
plt.close('all')
```

**Verification:**
```python
assert len(evoked.info['projs']) == 0
```

### Step 8: Call evoked.pick()

```python
evoked.pick(picks='meg')
```

### Step 9: Call evoked.add_proj()

```python
evoked.add_proj(compute_proj_evoked(evoked, n_mag=1, n_grad=1, meg='combined'))
```

**Verification:**
```python
assert len(evoked.info['projs']) == 1
```

### Step 10: Call evoked.plot_joint()

```python
evoked.plot_joint(ts_args=dict(proj='reconstruct'), topomap_args=dict(proj='reconstruct'))
```

### Step 11: Call evoked.del_proj.pick()

```python
evoked.del_proj().pick('mag')
```

### Step 12: Assign mapping = value

```python
mapping = {ch_name: 'seeg' for ch_name in evoked.ch_names}
```

### Step 13: Call evoked.set_channel_types()

```python
evoked.set_channel_types(mapping, on_unit_change='ignore')
```

### Step 14: Call evoked.plot_joint()

```python
evoked.plot_joint()
```

### Step 15: Assign evoked = _get_epochs.average.pick(...)

```python
evoked = _get_epochs().average().pick('mag')
```

### Step 16: Assign mapping = value

```python
mapping = {ch_name: 'dbs' for ch_name in evoked.ch_names}
```

### Step 17: Call evoked.set_channel_types()

```python
evoked.set_channel_types(mapping, on_unit_change='ignore')
```

### Step 18: Call evoked.plot_joint()

```python
evoked.plot_joint()
```

### Step 19: Call plt.close()

```python
plt.close('all')
```

### Step 20: Call evoked.plot_joint()

```python
evoked.plot_joint(ts_args=dict(axes=True, time_unit='s'))
```

### Step 21: Call evoked.plot_joint()

```python
evoked.plot_joint(picks=[6, 7, 8], ts_args=dict(axes=axes[0]), topomap_args=dict(axes=axes[2:]))
```

### Step 22: Call evoked.plot_joint()

```python
evoked.plot_joint(ts_args=dict(proj=True), topomap_args=dict(proj=False))
```


## Complete Example

```python
# Workflow
'Test joint plot.'
evoked = _get_epochs().average()
evoked.plot_joint(ts_args=dict(time_unit='s'), topomap_args=dict(time_unit='s'))

def return_inds(d):
    return list(range(d.shape[0]))
evoked.plot_joint(title='test', topomap_args=dict(contours=0, res=8, time_unit='ms'), ts_args=dict(spatial_colors=True, zorder=return_inds, time_unit='s'))
with pytest.raises(ValueError, match='If one of `ts_args` and'):
    evoked.plot_joint(ts_args=dict(axes=True, time_unit='s'))
axes = plt.subplots(nrows=3)[-1].flatten().tolist()
evoked.plot_joint(times=[0], picks=[6, 7, 8], ts_args=dict(axes=axes[0]), topomap_args={'axes': axes[1:], 'time_unit': 's'})
with pytest.raises(ValueError, match='of length 4'):
    evoked.plot_joint(picks=[6, 7, 8], ts_args=dict(axes=axes[0]), topomap_args=dict(axes=axes[2:]))
plt.close('all')
assert len(evoked.info['projs']) == 0
evoked.pick(picks='meg')
evoked.add_proj(compute_proj_evoked(evoked, n_mag=1, n_grad=1, meg='combined'))
assert len(evoked.info['projs']) == 1
with pytest.raises(ValueError, match='must match ts_args'):
    evoked.plot_joint(ts_args=dict(proj=True), topomap_args=dict(proj=False))
evoked.plot_joint(ts_args=dict(proj='reconstruct'), topomap_args=dict(proj='reconstruct'))
evoked.del_proj().pick('mag')
mapping = {ch_name: 'seeg' for ch_name in evoked.ch_names}
evoked.set_channel_types(mapping, on_unit_change='ignore')
evoked.plot_joint()
evoked = _get_epochs().average().pick('mag')
mapping = {ch_name: 'dbs' for ch_name in evoked.ch_names}
evoked.set_channel_types(mapping, on_unit_change='ignore')
evoked.plot_joint()
plt.close('all')
```

## Next Steps


---

*Source: test_topo.py:83 | Complexity: Advanced | Last updated: 2026-05-18*