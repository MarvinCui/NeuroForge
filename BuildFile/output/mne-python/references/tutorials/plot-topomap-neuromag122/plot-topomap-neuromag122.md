# How To: Plot Topomap Neuromag122

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test topomap plotting.

## Prerequisites

**Required Modules:**
- `functools`
- `pathlib`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.patches`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.time_frequency.tfr`
- `mne.viz`
- `mne.viz.tests.test_raw`
- `mne.viz.topomap`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test topomap plotting.'

```python
'Test topomap plotting.'
```

**Verification:**
```python
assert layout.kind.startswith('Neuromag_122')
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(evoked_fname, 'Left Auditory', baseline=(None, 0))
```

### Step 3: Call evoked.pick()

```python
evoked.pick(picks='grad')
```

### Step 4: Call evoked.pick()

```python
evoked.pick(evoked.ch_names[:122])
```

### Step 5: Assign ch_names = value

```python
ch_names = [f'MEG {k:03}' for k in range(1, 123)]
```

### Step 6: Call evoked.rename_channels()

```python
evoked.rename_channels({c_old: c_new for c_old, c_new in zip(evoked.ch_names, ch_names)})
```

### Step 7: Assign layout = find_layout(...)

```python
layout = find_layout(evoked.info)
```

**Verification:**
```python
assert layout.kind.startswith('Neuromag_122')
```

### Step 8: Call evoked.plot_topomap()

```python
evoked.plot_topomap(times=[0.1], **fast_test)
```

### Step 9: Assign proj = Projection(...)

```python
proj = Projection(active=False, desc='test', kind=1, data=dict(nrow=1, ncol=122, row_names=None, col_names=evoked.ch_names, data=np.ones(122)), explained_var=0.5)
```

### Step 10: Call plot_projs_topomap()

```python
plot_projs_topomap([proj], evoked.info, **fast_test)
```

### Step 11: Assign unknown = value

```python
c['coil_type'] = FIFF.FIFFV_COIL_NM_122
```


## Complete Example

```python
# Workflow
'Test topomap plotting.'
evoked = read_evokeds(evoked_fname, 'Left Auditory', baseline=(None, 0))
evoked.pick(picks='grad')
evoked.pick(evoked.ch_names[:122])
ch_names = [f'MEG {k:03}' for k in range(1, 123)]
for c in evoked.info['chs']:
    c['coil_type'] = FIFF.FIFFV_COIL_NM_122
evoked.rename_channels({c_old: c_new for c_old, c_new in zip(evoked.ch_names, ch_names)})
layout = find_layout(evoked.info)
assert layout.kind.startswith('Neuromag_122')
evoked.plot_topomap(times=[0.1], **fast_test)
proj = Projection(active=False, desc='test', kind=1, data=dict(nrow=1, ncol=122, row_names=None, col_names=evoked.ch_names, data=np.ones(122)), explained_var=0.5)
plot_projs_topomap([proj], evoked.info, **fast_test)
```

## Next Steps


---

*Source: test_topomap.py:715 | Complexity: Advanced | Last updated: 2026-05-18*