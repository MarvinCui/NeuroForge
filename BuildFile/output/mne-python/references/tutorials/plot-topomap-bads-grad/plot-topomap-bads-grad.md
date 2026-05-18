# How To: Plot Topomap Bads Grad

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting topomap with bad gradiometer channels (gh-8802).

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

### Step 1: 'Test plotting topomap with bad gradiometer channels (gh-8802).'

```python
'Test plotting topomap with bad gradiometer channels (gh-8802).'
```

**Verification:**
```python
assert len(info['chs']) == 203
```

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(203)
```

### Step 3: Assign info = read_info(...)

```python
info = read_info(evoked_fname)
```

### Step 4: Assign unknown = value

```python
info['bads'] = ['MEG 2242']
```

### Step 5: Assign picks = pick_types(...)

```python
picks = pick_types(info, meg='grad')
```

### Step 6: Assign info = pick_info(...)

```python
info = pick_info(info, picks)
```

**Verification:**
```python
assert len(info['chs']) == 203
```

### Step 7: Call plot_topomap()

```python
plot_topomap(data, info, res=8)
```


## Complete Example

```python
# Workflow
'Test plotting topomap with bad gradiometer channels (gh-8802).'
data = np.random.RandomState(0).randn(203)
info = read_info(evoked_fname)
info['bads'] = ['MEG 2242']
picks = pick_types(info, meg='grad')
info = pick_info(info, picks)
assert len(info['chs']) == 203
plot_topomap(data, info, res=8)
```

## Next Steps


---

*Source: test_topomap.py:776 | Complexity: Intermediate | Last updated: 2026-05-18*