# How To: Plotting Scalebars

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that raw scalebars are not overplotted.

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
# Fixtures: browser_backend, qtbot
```

## Step-by-Step Guide

### Step 1: 'Test that raw scalebars are not overplotted.'

```python
'Test that raw scalebars are not overplotted.'
```

**Verification:**
```python
assert ch_types == ['mag', 'grad', 'eeg', 'eog', 'stim']
```

### Step 2: Assign ismpl = value

```python
ismpl = browser_backend.name == 'matplotlib'
```

**Verification:**
```python
assert ch_types == ['grad', 'mag', 'eeg', 'eog', 'stim']
```

### Step 3: Assign raw = mne.io.read_raw_fif.crop.load_data(...)

```python
raw = mne.io.read_raw_fif(raw_fname).crop(0, 1).load_data()
```

**Verification:**
```python
assert ch_types.pop(-1) == 'stim'
```

### Step 4: Assign fig = raw.plot(...)

```python
fig = raw.plot(butterfly=True)
```

**Verification:**
```python
assert_allclose(yvals, [ci - delta, ci + delta], err_msg=err_msg)
```

### Step 5: Assign ch_types = value

```python
ch_types = [text.get_text() for text in fig.mne.ax_main.get_yticklabels()]
```

**Verification:**
```python
assert ch_types == ['mag', 'grad', 'eeg', 'eog', 'stim']
```

### Step 6: Assign delta = 0.25

```python
delta = 0.25
```

### Step 7: Assign offset = 0

```python
offset = 0
```

### Step 8: Call qtbot.wait_exposed()

```python
qtbot.wait_exposed(fig)
```

**Verification:**
```python
assert ch_types == ['grad', 'mag', 'eeg', 'eog', 'stim']
```

### Step 9: Assign delta = 0.5

```python
delta = 0.5
```

### Step 10: Assign offset = 1

```python
offset = 1
```

### Step 11: Assign err_msg = value

```python
err_msg = f'ch_type={ch_type!r} should be centered around y={ci}'
```

### Step 12: Assign this_bar = value

```python
this_bar = fig.mne.scalebars[ch_type]
```

### Step 13: Call assert_allclose()

```python
assert_allclose(yvals, [ci - delta, ci + delta], err_msg=err_msg)
```

### Step 14: Assign ch_types = list(...)

```python
ch_types = list(fig.mne.channel_axis.ch_texts)
```

### Step 15: Call qtbot.wait()

```python
qtbot.wait(100)
```

### Step 16: Assign yvals = value

```python
yvals = this_bar.get_data()[1]
```

### Step 17: Assign yvals = this_bar.get_ydata(...)

```python
yvals = this_bar.get_ydata()
```


## Complete Example

```python
# Setup
# Fixtures: browser_backend, qtbot

# Workflow
'Test that raw scalebars are not overplotted.'
ismpl = browser_backend.name == 'matplotlib'
raw = mne.io.read_raw_fif(raw_fname).crop(0, 1).load_data()
fig = raw.plot(butterfly=True)
if ismpl:
    ch_types = [text.get_text() for text in fig.mne.ax_main.get_yticklabels()]
    assert ch_types == ['mag', 'grad', 'eeg', 'eog', 'stim']
    delta = 0.25
    offset = 0
else:
    qtbot.wait_exposed(fig)
    for _ in range(10):
        ch_types = list(fig.mne.channel_axis.ch_texts)
        if len(ch_types) > 0:
            break
        qtbot.wait(100)
    assert ch_types == ['grad', 'mag', 'eeg', 'eog', 'stim']
    delta = 0.5
    offset = 1
assert ch_types.pop(-1) == 'stim'
for ci, ch_type in enumerate(ch_types, offset):
    err_msg = f'ch_type={ch_type!r} should be centered around y={ci}'
    this_bar = fig.mne.scalebars[ch_type]
    if ismpl:
        yvals = this_bar.get_data()[1]
    else:
        yvals = this_bar.get_ydata()
    assert_allclose(yvals, [ci - delta, ci + delta], err_msg=err_msg)
```

## Next Steps


---

*Source: test_raw.py:1337 | Complexity: Advanced | Last updated: 2026-05-18*