# How To: Plot White Rank

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_white with a combined-MEG rank arg.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.collections`
- `matplotlib.colors`
- `mpl_toolkits.axes_grid1.parasite_axes`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.stats.parametric`
- `mne.utils`
- `mne.viz`
- `mne.viz.utils`


## Step-by-Step Guide

### Step 1: 'Test plot_white with a combined-MEG rank arg.'

```python
'Test plot_white with a combined-MEG rank arg.'
```

**Verification:**
```python
assert 'grad' not in rank
```

### Step 2: Assign cov = read_cov(...)

```python
cov = read_cov(cov_fname)
```

**Verification:**
```python
assert 'mag' not in rank
```

### Step 3: Assign unknown = 'empirical'

```python
cov['method'] = 'empirical'
```

**Verification:**
```python
assert 'meg' in rank
```

### Step 4: Assign unknown = value

```python
cov['projs'] = []
```

### Step 5: Assign evoked = _get_epochs.average(...)

```python
evoked = _get_epochs().average()
```

### Step 6: Call evoked.set_eeg_reference()

```python
evoked.set_eeg_reference('average')
```

### Step 7: Assign rank = compute_rank(...)

```python
rank = compute_rank(evoked, 'info')
```

**Verification:**
```python
assert 'grad' not in rank
```

### Step 8: Call evoked.plot_white()

```python
evoked.plot_white(cov)
```

### Step 9: Call evoked.plot_white()

```python
evoked.plot_white(cov, rank=rank)
```


## Complete Example

```python
# Workflow
'Test plot_white with a combined-MEG rank arg.'
cov = read_cov(cov_fname)
cov['method'] = 'empirical'
cov['projs'] = []
evoked = _get_epochs().average()
evoked.set_eeg_reference('average')
rank = compute_rank(evoked, 'info')
assert 'grad' not in rank
assert 'mag' not in rank
assert 'meg' in rank
evoked.plot_white(cov)
evoked.plot_white(cov, rank=rank)
```

## Next Steps


---

*Source: test_evoked.py:361 | Complexity: Advanced | Last updated: 2026-05-18*