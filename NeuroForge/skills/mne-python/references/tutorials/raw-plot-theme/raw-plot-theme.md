# How To: Raw Plot Theme

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test dark/light theme for the matplotlib browser backend.

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
# Fixtures: theme, mpl_backend
```

## Step-by-Step Guide

### Step 1: 'Test dark/light theme for the matplotlib browser backend.'

```python
'Test dark/light theme for the matplotlib browser backend.'
```

**Verification:**
```python
assert _hex(fig.mne.bgcolor) == _DARK_BGCOLOR
```

### Step 2: Assign sfreq = 100.0

```python
sfreq = 100.0
```

**Verification:**
```python
assert _hex(fig.mne.fgcolor) == _DARK_FGCOLOR
```

### Step 3: Assign t = value

```python
t = np.arange(500) / sfreq
```

**Verification:**
```python
assert _hex(fig.mne.ch_color_bad) == _DARK_BAD_COLOR
```

### Step 4: Assign data = value

```python
data = np.sin(2 * np.pi * 1.0 * t)[np.newaxis, :]
```

**Verification:**
```python
assert _hex(fig.mne.ch_color_dict['eeg']) == _DARK_CHANNEL_OVERRIDES['eeg']
```

### Step 5: Assign info = create_info(...)

```python
info = create_info(['EEG 001'], sfreq, 'eeg')
```

**Verification:**
```python
assert _hex(fig.patch.get_facecolor()) == _DARK_BGCOLOR
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

**Verification:**
```python
assert _hex(fig.mne.ax_main.get_facecolor()) == _DARK_BGCOLOR
```

### Step 7: Assign fig = raw.plot(...)

```python
fig = raw.plot(theme=theme)
```

**Verification:**
```python
assert _hex(fig.mne.ax_hscroll.get_facecolor()) == _DARK_BGCOLOR
```

### Step 8: Call plt.close()

```python
plt.close('all')
```

**Verification:**
```python
assert _hex(fig.mne.bgcolor) == _hex('w')
```


## Complete Example

```python
# Setup
# Fixtures: theme, mpl_backend

# Workflow
'Test dark/light theme for the matplotlib browser backend.'
import matplotlib.colors as mcolors
from mne.viz._mpl_figure import _DARK_BAD_COLOR, _DARK_BGCOLOR, _DARK_CHANNEL_OVERRIDES, _DARK_FGCOLOR
sfreq = 100.0
t = np.arange(500) / sfreq
data = np.sin(2 * np.pi * 1.0 * t)[np.newaxis, :]
info = create_info(['EEG 001'], sfreq, 'eeg')
raw = RawArray(data, info)
fig = raw.plot(theme=theme)

def _hex(c):
    return mcolors.to_hex(c)
if theme == 'dark':
    assert _hex(fig.mne.bgcolor) == _DARK_BGCOLOR
    assert _hex(fig.mne.fgcolor) == _DARK_FGCOLOR
    assert _hex(fig.mne.ch_color_bad) == _DARK_BAD_COLOR
    assert _hex(fig.mne.ch_color_dict['eeg']) == _DARK_CHANNEL_OVERRIDES['eeg']
    assert _hex(fig.patch.get_facecolor()) == _DARK_BGCOLOR
    assert _hex(fig.mne.ax_main.get_facecolor()) == _DARK_BGCOLOR
    assert _hex(fig.mne.ax_hscroll.get_facecolor()) == _DARK_BGCOLOR
else:
    assert _hex(fig.mne.bgcolor) == _hex('w')
    assert _hex(fig.mne.ch_color_dict['eeg']) == _hex('k')
    assert _hex(fig.patch.get_facecolor()) == _hex('w')
    assert _hex(fig.mne.ax_main.get_facecolor()) == _hex('w')
plt.close('all')
```

## Next Steps


---

*Source: test_raw.py:1370 | Complexity: Advanced | Last updated: 2026-05-18*