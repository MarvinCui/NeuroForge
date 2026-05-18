# How To: Plot Psd Epochs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting epochs psd (+topomap).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.utils`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: epochs
```

## Step-by-Step Guide

### Step 1: 'Test plotting epochs psd (+topomap).'

```python
'Test plotting epochs psd (+topomap).'
```

**Verification:**
```python
assert len(fig.axes) == 10
```

### Step 2: Assign spectrum = epochs.compute_psd(...)

```python
spectrum = epochs.compute_psd()
```

**Verification:**
```python
assert all((vmin_0 == ax.images[0].norm.vmin for ax in fig.axes[1:5]))
```

### Step 3: Assign old_defaults = dict(...)

```python
old_defaults = dict(picks='data', exclude='bads')
```

**Verification:**
```python
assert all((vmax_0 == ax.images[0].norm.vmax for ax in fig.axes[1:5]))
```

### Step 4: Call spectrum.plot()

```python
spectrum.plot(average=True, amplitude=False, spatial_colors=False, **old_defaults)
```

### Step 5: Call spectrum.plot()

```python
spectrum.plot(average=False, amplitude=False, spatial_colors=True, **old_defaults)
```

### Step 6: Call spectrum.plot()

```python
spectrum.plot(average=False, amplitude=False, spatial_colors=False, **old_defaults)
```

### Step 7: Call plt.close()

```python
plt.close('all')
```

### Step 8: Assign fig = spectrum.plot_topomap(...)

```python
fig = spectrum.plot_topomap()
```

**Verification:**
```python
assert len(fig.axes) == 10
```

### Step 9: Assign fig = spectrum.plot_topomap(...)

```python
fig = spectrum.plot_topomap(vlim='joint')
```

### Step 10: Assign vmin_0 = value

```python
vmin_0 = fig.axes[0].images[0].norm.vmin
```

### Step 11: Assign vmax_0 = value

```python
vmax_0 = fig.axes[0].images[0].norm.vmax
```

**Verification:**
```python
assert all((vmin_0 == ax.images[0].norm.vmin for ax in fig.axes[1:5]))
```

### Step 12: Assign fig = spectrum.plot_topomap(...)

```python
fig = spectrum.plot_topomap(bands=[(20, '20 Hz'), (15, 25, '15-25 Hz')])
```

### Step 13: Assign err_str = value

```python
err_str = f'for channel {epochs.ch_names[2]}'
```

### Step 14: Assign unknown = 0

```python
epochs.get_data(copy=False)[0, 2, :] = 0
```

### Step 15: Call spectrum.plot_topomap()

```python
spectrum.plot_topomap(bands=dict(foo=(0, 0.01)))
```

### Step 16: Call epochs.compute_psd.plot()

```python
epochs.compute_psd().plot(dB=dB)
```


## Complete Example

```python
# Setup
# Fixtures: epochs

# Workflow
'Test plotting epochs psd (+topomap).'
spectrum = epochs.compute_psd()
old_defaults = dict(picks='data', exclude='bads')
spectrum.plot(average=True, amplitude=False, spatial_colors=False, **old_defaults)
spectrum.plot(average=False, amplitude=False, spatial_colors=True, **old_defaults)
spectrum.plot(average=False, amplitude=False, spatial_colors=False, **old_defaults)
with pytest.raises(RuntimeError, match='No frequencies in band'):
    spectrum.plot_topomap(bands=dict(foo=(0, 0.01)))
plt.close('all')
fig = spectrum.plot_topomap()
assert len(fig.axes) == 10
fig = spectrum.plot_topomap(vlim='joint')
vmin_0 = fig.axes[0].images[0].norm.vmin
vmax_0 = fig.axes[0].images[0].norm.vmax
assert all((vmin_0 == ax.images[0].norm.vmin for ax in fig.axes[1:5]))
assert all((vmax_0 == ax.images[0].norm.vmax for ax in fig.axes[1:5]))
fig = spectrum.plot_topomap(bands=[(20, '20 Hz'), (15, 25, '15-25 Hz')])
err_str = f'for channel {epochs.ch_names[2]}'
epochs.get_data(copy=False)[0, 2, :] = 0
for dB in [True, False]:
    with _record_warnings(), pytest.warns(UserWarning, match=err_str):
        epochs.compute_psd().plot(dB=dB)
```

## Next Steps


---

*Source: test_epochs.py:397 | Complexity: Advanced | Last updated: 2026-05-18*