# How To: Plot Topomap Animation Csd

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test topomap plotting of CSD data.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: capsys
```

## Step-by-Step Guide

### Step 1: 'Test topomap plotting of CSD data.'

```python
'Test topomap plotting of CSD data.'
```

**Verification:**
```python
assert 'extrapolation mode head to 0' in out
```

### Step 2: Assign evoked = read_evokeds(...)

```python
evoked = read_evokeds(evoked_fname, 'Left Auditory', baseline=(None, 0))
```

### Step 3: Assign evoked_csd = compute_current_source_density(...)

```python
evoked_csd = compute_current_source_density(evoked)
```

### Step 4: Assign unknown = evoked_csd.animate_topomap(...)

```python
_, anim = evoked_csd.animate_topomap(ch_type='csd', times=[0, 0.1], butterfly=False, time_unit='s', verbose='debug')
```

### Step 5: Call anim._func()

```python
anim._func(1)
```

### Step 6: Assign unknown = capsys.readouterr(...)

```python
out, _ = capsys.readouterr()
```

**Verification:**
```python
assert 'extrapolation mode head to 0' in out
```


## Complete Example

```python
# Setup
# Fixtures: capsys

# Workflow
'Test topomap plotting of CSD data.'
evoked = read_evokeds(evoked_fname, 'Left Auditory', baseline=(None, 0))
evoked_csd = compute_current_source_density(evoked)
_, anim = evoked_csd.animate_topomap(ch_type='csd', times=[0, 0.1], butterfly=False, time_unit='s', verbose='debug')
anim._func(1)
out, _ = capsys.readouterr()
assert 'extrapolation mode head to 0' in out
```

## Next Steps


---

*Source: test_topomap.py:192 | Complexity: Intermediate | Last updated: 2026-05-18*