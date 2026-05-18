# How To: Plot Topomap Channel Distance

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test topomap plotting with spread out channels (gh-9511, gh-9526).

Test topomap plotting when the distance between channels is greater than
the head radius.

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

### Step 1: '\n    Test topomap plotting with spread out channels (gh-9511, gh-9526).\n\n    Test topomap plotting when the distance between channels is greater than\n    the head radius.\n    '

```python
'\n    Test topomap plotting with spread out channels (gh-9511, gh-9526).\n\n    Test topomap plotting when the distance between channels is greater than\n    the head radius.\n    '
```

### Step 2: Assign ch_names = value

```python
ch_names = ['TP9', 'AF7', 'AF8', 'TP10']
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(ch_names, 100, ch_types='eeg')
```

### Step 4: Assign evoked = EvokedArray(...)

```python
evoked = EvokedArray(np.random.randn(4, 10) * 1e-06, info)
```

### Step 5: Assign ten_five = make_standard_montage(...)

```python
ten_five = make_standard_montage('standard_1005')
```

### Step 6: Call evoked.set_montage()

```python
evoked.set_montage(ten_five)
```

### Step 7: Call evoked.plot_topomap()

```python
evoked.plot_topomap(sphere=0.05, res=8)
```


## Complete Example

```python
# Workflow
'\n    Test topomap plotting with spread out channels (gh-9511, gh-9526).\n\n    Test topomap plotting when the distance between channels is greater than\n    the head radius.\n    '
ch_names = ['TP9', 'AF7', 'AF8', 'TP10']
info = create_info(ch_names, 100, ch_types='eeg')
evoked = EvokedArray(np.random.randn(4, 10) * 1e-06, info)
ten_five = make_standard_montage('standard_1005')
evoked.set_montage(ten_five)
evoked.plot_topomap(sphere=0.05, res=8)
```

## Next Steps


---

*Source: test_topomap.py:759 | Complexity: Intermediate | Last updated: 2026-05-18*