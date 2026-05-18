# How To: Plot Spectrum

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting EpochsSpectrum(Array).

Testing Spectrum(Array) with raw data doesn't improve coverage.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: method, output, average, request
```

## Step-by-Step Guide

### Step 1: "Test plotting EpochsSpectrum(Array).\n\n    Testing Spectrum(Array) with raw data doesn't improve coverage.\n    "

```python
"Test plotting EpochsSpectrum(Array).\n\n    Testing Spectrum(Array) with raw data doesn't improve coverage.\n    "
```

**Verification:**
```python
assert len(lines) == n_grad
```

### Step 2: Assign unknown = value

```python
spectrum.info['bads'] = spectrum.ch_names[:1]
```

**Verification:**
```python
assert n_bad == 1
```

### Step 3: Call spectrum.plot()

```python
spectrum.plot(average=True, amplitude=True, spatial_colors=True)
```

### Step 4: Call spectrum.plot()

```python
spectrum.plot(average=True, amplitude=False, spatial_colors=False)
```

### Step 5: Assign n_grad = sum(...)

```python
n_grad = sum((ch_type == 'grad' for ch_type in spectrum.get_channel_types()))
```

### Step 6: Call spectrum.plot_topo()

```python
spectrum.plot_topo()
```

### Step 7: Call spectrum.plot_topomap()

```python
spectrum.plot_topomap()
```

### Step 8: Assign spectrum = request.getfixturevalue(...)

```python
spectrum = request.getfixturevalue('epochs_spectrum')
```

### Step 9: Assign data = request.getfixturevalue(...)

```python
data = request.getfixturevalue('epochs')
```

### Step 10: Assign kwargs = dict(...)

```python
kwargs = dict()
```

### Step 11: Assign spectrum = data.compute_psd(...)

```python
spectrum = data.compute_psd(method=method, output=output, **kwargs)
```

### Step 12: Assign fig = spectrum.plot(...)

```python
fig = spectrum.plot(average=False, amplitude=amp, spatial_colors=sc, exclude=())
```

### Step 13: Assign lines = value

```python
lines = fig.axes[0].lines[2:]
```

**Verification:**
```python
assert len(lines) == n_grad
```

### Step 14: Assign bad_color = value

```python
bad_color = '0.5' if sc else 'r'
```

### Step 15: Assign n_bad = sum(...)

```python
n_bad = sum((same_color(line.get_color(), bad_color) for line in lines))
```

**Verification:**
```python
assert n_bad == 1
```

### Step 16: Call kwargs.update()

```python
kwargs.update(average=average)
```


## Complete Example

```python
# Setup
# Fixtures: method, output, average, request

# Workflow
"Test plotting EpochsSpectrum(Array).\n\n    Testing Spectrum(Array) with raw data doesn't improve coverage.\n    "
if method == 'welch' and output == 'power' and average:
    spectrum = request.getfixturevalue('epochs_spectrum')
else:
    data = request.getfixturevalue('epochs')
    kwargs = dict()
    if method == 'welch':
        kwargs.update(average=average)
    spectrum = data.compute_psd(method=method, output=output, **kwargs)
spectrum.info['bads'] = spectrum.ch_names[:1]
spectrum.plot(average=True, amplitude=True, spatial_colors=True)
spectrum.plot(average=True, amplitude=False, spatial_colors=False)
n_grad = sum((ch_type == 'grad' for ch_type in spectrum.get_channel_types()))
for amp, sc in ((True, True), (False, False)):
    fig = spectrum.plot(average=False, amplitude=amp, spatial_colors=sc, exclude=())
    lines = fig.axes[0].lines[2:]
    assert len(lines) == n_grad
    bad_color = '0.5' if sc else 'r'
    n_bad = sum((same_color(line.get_color(), bad_color) for line in lines))
    assert n_bad == 1
spectrum.plot_topo()
spectrum.plot_topomap()
```

## Next Steps


---

*Source: test_spectrum.py:696 | Complexity: Advanced | Last updated: 2026-05-18*