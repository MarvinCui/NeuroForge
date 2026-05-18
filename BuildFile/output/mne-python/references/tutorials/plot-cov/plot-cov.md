# How To: Plot Cov

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of covariances.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test plotting of covariances.'

```python
'Test plotting of covariances.'
```

### Step 2: Assign raw = _get_raw(...)

```python
raw = _get_raw()
```

### Step 3: Assign cov = read_cov(...)

```python
cov = read_cov(cov_fname)
```

### Step 4: Assign unknown = value

```python
cov['data'] = cov.data * (1 + 1j)
```

### Step 5: Assign unknown = cov.plot(...)

```python
fig1, fig2 = cov.plot(raw.info)
```

### Step 6: Call raw.del_proj()

```python
raw.del_proj('all')
```

### Step 7: Call raw.set_channel_types()

```python
raw.set_channel_types({ch: 'misc' for ch in raw.ch_names}, on_unit_change='ignore')
```

### Step 8: Assign unknown = cov.plot(...)

```python
fig1, fig2 = cov.plot(raw.info, proj=True, exclude=raw.ch_names[6:])
```

### Step 9: Call cov.plot()

```python
cov.plot(raw.info, exclude=raw.ch_names[6:])
```


## Complete Example

```python
# Workflow
'Test plotting of covariances.'
raw = _get_raw()
cov = read_cov(cov_fname)
with pytest.warns(RuntimeWarning, match='projection'):
    fig1, fig2 = cov.plot(raw.info, proj=True, exclude=raw.ch_names[6:])
cov['data'] = cov.data * (1 + 1j)
fig1, fig2 = cov.plot(raw.info)
raw.del_proj('all')
raw.set_channel_types({ch: 'misc' for ch in raw.ch_names}, on_unit_change='ignore')
with pytest.raises(RuntimeError, match='No plottable channel types found'):
    cov.plot(raw.info, exclude=raw.ch_names[6:])
```

## Next Steps


---

*Source: test_misc.py:128 | Complexity: Advanced | Last updated: 2026-05-18*