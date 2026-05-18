# How To: Plotting Temperature Gsr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can plot temperature and GSR.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `os`
- `copy`
- `pathlib`
- `matplotlib.colors`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.pick`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`
- `mne.viz._mpl_figure`
- `cycler`
- `matplotlib.colors`
- `mne_qt_browser`
- `mne_qt_browser._pg_figure`
- `matplotlib.colors`
- `mne.viz._mpl_figure`
- `matplotlib.colors`
- `mne.viz._mpl_figure`
- `mne.viz._mpl_figure`

**Setup Required:**
```python
# Fixtures: browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test that we can plot temperature and GSR.'

```python
'Test that we can plot temperature and GSR.'
```

**Verification:**
```python
assert len(tick_texts) == 2
```

### Step 2: Assign data = np.random.RandomState.randn(...)

```python
data = np.random.RandomState(0).randn(2, 1000)
```

### Step 3: Assign info = create_info(...)

```python
info = create_info(2, 1000.0, ['temperature', 'gsr'])
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 5: Assign fig = raw.plot(...)

```python
fig = raw.plot()
```

### Step 6: Assign tick_texts = fig._get_ticklabels(...)

```python
tick_texts = fig._get_ticklabels('y')
```

**Verification:**
```python
assert len(tick_texts) == 2
```


## Complete Example

```python
# Setup
# Fixtures: browser_backend

# Workflow
'Test that we can plot temperature and GSR.'
data = np.random.RandomState(0).randn(2, 1000)
data[0] += 37
info = create_info(2, 1000.0, ['temperature', 'gsr'])
raw = RawArray(data, info)
fig = raw.plot()
tick_texts = fig._get_ticklabels('y')
assert len(tick_texts) == 2
```

## Next Steps


---

*Source: test_raw.py:1313 | Complexity: Intermediate | Last updated: 2026-05-18*