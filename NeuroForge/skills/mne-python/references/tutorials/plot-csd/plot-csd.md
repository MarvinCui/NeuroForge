# How To: Plot Csd

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plotting of CSD matrices.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.chpi`
- `mne.datasets`
- `mne.filter`
- `mne.io`
- `mne.minimum_norm`
- `mne.time_frequency`
- `mne.utils`
- `mne.viz`
- `mne.viz.misc`
- `mne.viz.utils`

**Setup Required:**
```python
# Fixtures: ch_types
```

## Step-by-Step Guide

### Step 1: 'Test plotting of CSD matrices.'

```python
'Test plotting of CSD matrices.'
```

**Verification:**
```python
assert len(figs) == expected_n_figs
```

### Step 2: Assign ch_names = value

```python
ch_names = [f'CH{i + 1}' for i in range(n_ch)]
```

### Step 3: Assign n_data = value

```python
n_data = n_ch * (n_ch + 1) // 2
```

### Step 4: Assign csd = CrossSpectralDensity(...)

```python
csd = CrossSpectralDensity(np.arange(1, n_data + 1), ch_names, frequencies=[(10, 20)], n_fft=1, tmin=0, tmax=1)
```

### Step 5: Assign n_ch_types = len(...)

```python
n_ch_types = len(ch_types)
```

### Step 6: Assign n_ch = value

```python
n_ch = 2 * n_ch_types
```

### Step 7: Assign ch_types = np.repeat.tolist(...)

```python
ch_types = np.repeat(ch_types, 2).tolist()
```

### Step 8: Assign n_ch = 2

```python
n_ch = 2
```

### Step 9: Assign info = None

```python
info = None
```

### Step 10: Assign expected_n_figs = 1

```python
expected_n_figs = 1
```

### Step 11: Assign info = create_info(...)

```python
info = create_info(ch_names, sfreq=1.0, ch_types=ch_types)
```

### Step 12: Assign unique_types = value

```python
unique_types = set(ch_types) if isinstance(ch_types, list) else {ch_types}
```

### Step 13: Assign expected_n_figs = len(...)

```python
expected_n_figs = len(unique_types)
```

### Step 14: Assign figs = plot_csd(...)

```python
figs = plot_csd(csd, info=info, mode=mode, show=False)
```

**Verification:**
```python
assert len(figs) == expected_n_figs
```

### Step 15: Call plot_csd()

```python
plot_csd(csd, info=info, mode=mode, show=False)
```


## Complete Example

```python
# Setup
# Fixtures: ch_types

# Workflow
'Test plotting of CSD matrices.'
if isinstance(ch_types, list):
    n_ch_types = len(ch_types)
    n_ch = 2 * n_ch_types
    ch_types = np.repeat(ch_types, 2).tolist()
else:
    n_ch = 2
ch_names = [f'CH{i + 1}' for i in range(n_ch)]
n_data = n_ch * (n_ch + 1) // 2
csd = CrossSpectralDensity(np.arange(1, n_data + 1), ch_names, frequencies=[(10, 20)], n_fft=1, tmin=0, tmax=1)
if ch_types is None:
    info = None
    expected_n_figs = 1
else:
    info = create_info(ch_names, sfreq=1.0, ch_types=ch_types)
    unique_types = set(ch_types) if isinstance(ch_types, list) else {ch_types}
    expected_n_figs = len(unique_types)
for mode in ('csd', 'coh'):
    if ch_types == 'misc':
        with pytest.raises(RuntimeError, match='No plottable channel types'):
            plot_csd(csd, info=info, mode=mode, show=False)
    else:
        figs = plot_csd(csd, info=info, mode=mode, show=False)
        assert len(figs) == expected_n_figs
```

## Next Steps


---

*Source: test_misc.py:332 | Complexity: Advanced | Last updated: 2026-05-18*