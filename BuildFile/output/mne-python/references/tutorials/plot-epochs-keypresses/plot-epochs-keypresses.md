# How To: Plot Epochs Keypresses

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plot_epochs keypress interaction.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.event`
- `mne.utils`
- `mne.viz`

**Setup Required:**
```python
# Fixtures: epochs_full, browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test plot_epochs keypress interaction.'

```python
'Test plot_epochs keypress interaction.'
```

### Step 2: Call epochs_full.drop_bad()

```python
epochs_full.drop_bad(dict(mag=4e-12))
```

### Step 3: Assign fig = epochs_full.plot(...)

```python
fig = epochs_full.plot(n_epochs=3)
```

### Step 4: Assign sample_idx = value

```python
sample_idx = len(epochs_full.times) // 2
```

### Step 5: Assign x = value

```python
x = fig.mne.traces[0].get_xdata()[sample_idx]
```

### Step 6: Assign y = value

```python
y = (fig.mne.traces[0].get_ydata()[sample_idx] + fig.mne.traces[1].get_ydata()[sample_idx]) / 2
```

### Step 7: Call fig._fake_click()

```python
fig._fake_click([x, y], xform='data')
```

### Step 8: Assign keys = value

```python
keys = ('pagedown', 'down', 'up', 'down', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'home', 'shift+right', 'end', 'shift+left', 'z', 'z', 's', 's', '?', 'h', 'j', 'b')
```

### Step 9: Call fig._fake_click()

```python
fig._fake_click([x, y], xform='data', button=3)
```

### Step 10: Call fig._fake_keypress()

```python
fig._fake_keypress(key)
```


## Complete Example

```python
# Setup
# Fixtures: epochs_full, browser_backend

# Workflow
'Test plot_epochs keypress interaction.'
epochs_full.drop_bad(dict(mag=4e-12))
fig = epochs_full.plot(n_epochs=3)
sample_idx = len(epochs_full.times) // 2
x = fig.mne.traces[0].get_xdata()[sample_idx]
y = (fig.mne.traces[0].get_ydata()[sample_idx] + fig.mne.traces[1].get_ydata()[sample_idx]) / 2
fig._fake_click([x, y], xform='data')
keys = ('pagedown', 'down', 'up', 'down', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'home', 'shift+right', 'end', 'shift+left', 'z', 'z', 's', 's', '?', 'h', 'j', 'b')
for key in keys * 2:
    fig._fake_keypress(key)
fig._fake_click([x, y], xform='data', button=3)
```

## Next Steps


---

*Source: test_epochs.py:164 | Complexity: Advanced | Last updated: 2026-05-18*