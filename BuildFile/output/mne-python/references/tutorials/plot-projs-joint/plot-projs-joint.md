# How To: Plot Projs Joint

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_projs_joint.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.viz`


## Step-by-Step Guide

### Step 1: 'Test plot_projs_joint.'

```python
'Test plot_projs_joint.'
```

**Verification:**
```python
assert len(evoked.ch_names) == n_mag + n_grad + n_eeg
```

### Step 2: Assign evoked = unknown.apply_baseline(...)

```python
evoked = read_evokeds(evoked_fname)[0].apply_baseline((None, 0))
```

**Verification:**
```python
assert evoked.get_channel_types(unique=True) == ['grad', 'eeg', 'mag']
```

### Step 3: Assign unknown = value

```python
evoked.info['bads'] = []
```

**Verification:**
```python
assert len(projs) == 5
```

### Step 4: Assign unknown = value

```python
n_mag, n_grad, n_eeg = (9, 10, 11)
```

**Verification:**
```python
assert ylab.startswith('Grad'), ylab
```

### Step 5: Assign unknown = value

```python
n_mag_proj, n_grad_proj, n_eeg_proj = (2, 2, 1)
```

**Verification:**
```python
assert ylab.startswith('EEG'), ylab
```

### Step 6: Assign picks = np.concatenate(...)

```python
picks = np.concatenate([pick_types(evoked.info, meg='grad')[:n_grad], pick_types(evoked.info, meg=False, eeg=True)[:n_eeg], pick_types(evoked.info, meg='mag')[:n_mag]])
```

**Verification:**
```python
assert ylab.startswith('Mag'), ylab
```

### Step 7: Call evoked.pick()

```python
evoked.pick(picks)
```

**Verification:**
```python
assert mag_trace_ax.get_ylabel() == ''
```

### Step 8: Assign projs = compute_proj_evoked(...)

```python
projs = compute_proj_evoked(evoked, n_mag=n_mag_proj, n_grad=n_grad_proj, n_eeg=n_eeg_proj)
```

**Verification:**
```python
assert len(mag_trace_ax.lines) == n_mag + 2 * n_mag_proj
```

### Step 9: Assign topomap_kwargs = dict(...)

```python
topomap_kwargs = dict(res=8, contours=0, sensors=False)
```

**Verification:**
```python
assert len(fig.axes) == 11
```

### Step 10: Assign fig = plot_projs_joint(...)

```python
fig = plot_projs_joint(projs, evoked, topomap_kwargs=topomap_kwargs, verbose='error')
```

**Verification:**
```python
assert len(fig.axes[mag_trace_ax_idx].lines) == old_len + 1
```

### Step 11: Assign ylab = unknown.get_ylabel(...)

```python
ylab = fig.axes[0].get_ylabel()
```

**Verification:**
```python
assert ylab.startswith('Grad'), ylab
```

### Step 12: Assign ylab = unknown.get_ylabel(...)

```python
ylab = fig.axes[4].get_ylabel()
```

**Verification:**
```python
assert ylab.startswith('EEG'), ylab
```

### Step 13: Assign ylab = unknown.get_ylabel(...)

```python
ylab = fig.axes[7].get_ylabel()
```

**Verification:**
```python
assert ylab.startswith('Mag'), ylab
```

### Step 14: Assign mag_trace_ax_idx = 10

```python
mag_trace_ax_idx = 10
```

### Step 15: Assign mag_trace_ax = value

```python
mag_trace_ax = fig.axes[mag_trace_ax_idx]
```

**Verification:**
```python
assert mag_trace_ax.get_ylabel() == ''
```

### Step 16: Assign old_len = len(...)

```python
old_len = len(mag_trace_ax.lines)
```

**Verification:**
```python
assert len(fig.axes) == 11
```

### Step 17: Assign fig = plot_projs_joint(...)

```python
fig = plot_projs_joint(projs, evoked, picks_trace='MEG 0111', topomap_kwargs=topomap_kwargs, verbose='error')
```

**Verification:**
```python
assert len(fig.axes[mag_trace_ax_idx].lines) == old_len + 1
```

### Step 18: Call evoked.crop.decimate()

```python
evoked.crop(-0.1, 0.1).decimate(10)
```


## Complete Example

```python
# Workflow
'Test plot_projs_joint.'
evoked = read_evokeds(evoked_fname)[0].apply_baseline((None, 0))
evoked.info['bads'] = []
n_mag, n_grad, n_eeg = (9, 10, 11)
n_mag_proj, n_grad_proj, n_eeg_proj = (2, 2, 1)
picks = np.concatenate([pick_types(evoked.info, meg='grad')[:n_grad], pick_types(evoked.info, meg=False, eeg=True)[:n_eeg], pick_types(evoked.info, meg='mag')[:n_mag]])
evoked.pick(picks)
assert len(evoked.ch_names) == n_mag + n_grad + n_eeg
assert evoked.get_channel_types(unique=True) == ['grad', 'eeg', 'mag']
projs = compute_proj_evoked(evoked, n_mag=n_mag_proj, n_grad=n_grad_proj, n_eeg=n_eeg_proj)
assert len(projs) == 5
with pytest.warns(RuntimeWarning, match='aliasing'):
    evoked.crop(-0.1, 0.1).decimate(10)
topomap_kwargs = dict(res=8, contours=0, sensors=False)
fig = plot_projs_joint(projs, evoked, topomap_kwargs=topomap_kwargs, verbose='error')
ylab = fig.axes[0].get_ylabel()
assert ylab.startswith('Grad'), ylab
ylab = fig.axes[4].get_ylabel()
assert ylab.startswith('EEG'), ylab
ylab = fig.axes[7].get_ylabel()
assert ylab.startswith('Mag'), ylab
mag_trace_ax_idx = 10
mag_trace_ax = fig.axes[mag_trace_ax_idx]
assert mag_trace_ax.get_ylabel() == ''
assert len(mag_trace_ax.lines) == n_mag + 2 * n_mag_proj
old_len = len(mag_trace_ax.lines)
assert len(fig.axes) == 11
fig = plot_projs_joint(projs, evoked, picks_trace='MEG 0111', topomap_kwargs=topomap_kwargs, verbose='error')
assert len(fig.axes[mag_trace_ax_idx].lines) == old_len + 1
```

## Next Steps


---

*Source: test_proj.py:18 | Complexity: Advanced | Last updated: 2026-05-18*