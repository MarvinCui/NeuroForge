# How To: Tfr Plot Joint

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test {Raw,Epochs,Average}TFR.plot_joint().

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `itertools`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.collections`
- `numpy.testing`
- `mne`
- `mne`
- `mne.epochs`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.tfr`
- `mne.utils`
- `mne.utils._testing`
- `mne.viz.utils`
- `test_spectrum`
- `pandas.testing`

**Setup Required:**
```python
# Fixtures: inst, ch_type, combine, timefreqs, title, full_average_tfr, request
```

## Step-by-Step Guide

### Step 1: 'Test {Raw,Epochs,Average}TFR.plot_joint().'

```python
'Test {Raw,Epochs,Average}TFR.plot_joint().'
```

**Verification:**
```python
assert f'Plotting topomap for {ch_type} data' in log.getvalue()
```

### Step 2: Assign tfr = _get_inst(...)

```python
tfr = _get_inst(inst, request, average_tfr=full_average_tfr)
```

**Verification:**
```python
assert len(fig.axes) == n_topomaps + 2
```

### Step 3: Assign n_topomaps = value

```python
n_topomaps = 1 if timefreqs is None else len(timefreqs)
```

**Verification:**
```python
assert fig.axes[0].get_title() == title
```

### Step 4: Assign ax = value

```python
ax = [ax for ax in fig.axes if ax.get_xlabel() == 'Time (s)'][0]
```

**Verification:**
```python
assert len(fignums) == 2
```

### Step 5: Assign kw = dict(...)

```python
kw = dict(fig=fig, ax=ax, xform='ax')
```

**Verification:**
```python
assert re.match('-?\\d{1,2}\\.\\d{3} - -?\\d{1,2}\\.\\d{3} s,\\n\\d{1,2}\\.\\d{2} - \\d{1,2}\\.\\d{2} Hz', _get_suptitle(popup_fig))
```

### Step 6: Call _fake_click()

```python
_fake_click(**kw, kind='press', point=(0.4, 0.4))
```

### Step 7: Call _fake_click()

```python
_fake_click(**kw, kind='motion', point=(0.5, 0.5))
```

### Step 8: Call _fake_click()

```python
_fake_click(**kw, kind='release', point=(0.6, 0.6))
```

### Step 9: Assign fignums = plt.get_fignums(...)

```python
fignums = plt.get_fignums()
```

**Verification:**
```python
assert len(fignums) == 2
```

### Step 10: Assign popup_fig = plt.figure(...)

```python
popup_fig = plt.figure(fignums[-1])
```

**Verification:**
```python
assert re.match('-?\\d{1,2}\\.\\d{3} - -?\\d{1,2}\\.\\d{3} s,\\n\\d{1,2}\\.\\d{2} - \\d{1,2}\\.\\d{2} Hz', _get_suptitle(popup_fig))
```

### Step 11: Assign fig = tfr.plot_joint(...)

```python
fig = tfr.plot_joint(picks=ch_type, timefreqs=timefreqs, combine=combine, topomap_args=dict(res=8, contours=0, sensors=False), verbose='debug')
```

**Verification:**
```python
assert f'Plotting topomap for {ch_type} data' in log.getvalue()
```


## Complete Example

```python
# Setup
# Fixtures: inst, ch_type, combine, timefreqs, title, full_average_tfr, request

# Workflow
'Test {Raw,Epochs,Average}TFR.plot_joint().'
tfr = _get_inst(inst, request, average_tfr=full_average_tfr)
with catch_logging() as log:
    fig = tfr.plot_joint(picks=ch_type, timefreqs=timefreqs, combine=combine, topomap_args=dict(res=8, contours=0, sensors=False), verbose='debug')
    assert f'Plotting topomap for {ch_type} data' in log.getvalue()
n_topomaps = 1 if timefreqs is None else len(timefreqs)
assert len(fig.axes) == n_topomaps + 2
if title is not None:
    assert fig.axes[0].get_title() == title
ax = [ax for ax in fig.axes if ax.get_xlabel() == 'Time (s)'][0]
kw = dict(fig=fig, ax=ax, xform='ax')
_fake_click(**kw, kind='press', point=(0.4, 0.4))
_fake_click(**kw, kind='motion', point=(0.5, 0.5))
_fake_click(**kw, kind='release', point=(0.6, 0.6))
fignums = plt.get_fignums()
assert len(fignums) == 2
popup_fig = plt.figure(fignums[-1])
assert re.match('-?\\d{1,2}\\.\\d{3} - -?\\d{1,2}\\.\\d{3} s,\\n\\d{1,2}\\.\\d{2} - \\d{1,2}\\.\\d{2} Hz', _get_suptitle(popup_fig))
```

## Next Steps


---

*Source: test_tfr.py:923 | Complexity: Advanced | Last updated: 2026-05-18*