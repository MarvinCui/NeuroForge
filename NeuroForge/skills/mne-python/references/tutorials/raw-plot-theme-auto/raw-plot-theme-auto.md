# How To: Raw Plot Theme Auto

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test theme="auto" resolves via _resolve_mpl_theme for the mpl backend.

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
# Fixtures: mpl_backend, monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test theme="auto" resolves via _resolve_mpl_theme for the mpl backend.'

```python
'Test theme="auto" resolves via _resolve_mpl_theme for the mpl backend.'
```

**Verification:**
```python
assert mcolors.to_hex(fig.mne.bgcolor) == _DARK_BGCOLOR
```

### Step 2: Assign sfreq = 100.0

```python
sfreq = 100.0
```

**Verification:**
```python
assert mcolors.to_hex(fig.mne.bgcolor) == mcolors.to_hex('w')
```

### Step 3: Assign t = value

```python
t = np.arange(500) / sfreq
```

### Step 4: Assign data = value

```python
data = np.sin(2 * np.pi * 1.0 * t)[np.newaxis, :]
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(['EEG 001'], sfreq, 'eeg')
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

### Step 7: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mpl_fig, '_resolve_mpl_theme', lambda theme: 'dark')
```

### Step 8: Assign fig = raw.plot(...)

```python
fig = raw.plot(theme='auto')
```

**Verification:**
```python
assert mcolors.to_hex(fig.mne.bgcolor) == _DARK_BGCOLOR
```

### Step 9: Call plt.close()

```python
plt.close('all')
```

### Step 10: Call monkeypatch.setattr()

```python
monkeypatch.setattr(mpl_fig, '_resolve_mpl_theme', lambda theme: 'light')
```

### Step 11: Assign fig = raw.plot(...)

```python
fig = raw.plot(theme='auto')
```

**Verification:**
```python
assert mcolors.to_hex(fig.mne.bgcolor) == mcolors.to_hex('w')
```

### Step 12: Call plt.close()

```python
plt.close('all')
```


## Complete Example

```python
# Setup
# Fixtures: mpl_backend, monkeypatch

# Workflow
'Test theme="auto" resolves via _resolve_mpl_theme for the mpl backend.'
import matplotlib.colors as mcolors
import mne.viz._mpl_figure as mpl_fig
from mne.viz._mpl_figure import _DARK_BGCOLOR
sfreq = 100.0
t = np.arange(500) / sfreq
data = np.sin(2 * np.pi * 1.0 * t)[np.newaxis, :]
info = create_info(['EEG 001'], sfreq, 'eeg')
raw = RawArray(data, info)
monkeypatch.setattr(mpl_fig, '_resolve_mpl_theme', lambda theme: 'dark')
fig = raw.plot(theme='auto')
assert mcolors.to_hex(fig.mne.bgcolor) == _DARK_BGCOLOR
plt.close('all')
monkeypatch.setattr(mpl_fig, '_resolve_mpl_theme', lambda theme: 'light')
fig = raw.plot(theme='auto')
assert mcolors.to_hex(fig.mne.bgcolor) == mcolors.to_hex('w')
plt.close('all')
```

## Next Steps


---

*Source: test_raw.py:1407 | Complexity: Advanced | Last updated: 2026-05-18*