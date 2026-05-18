# How To: Plot Instance Components

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test plotting of components as instances of raw and epochs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.io`
- `mne.preprocessing`
- `mne.utils`
- `mne.viz.ica`
- `mne.viz.utils`

**Setup Required:**
```python
# Fixtures: browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test plotting of components as instances of raw and epochs.'

```python
'Test plotting of components as instances of raw and epochs.'
```

### Step 2: Assign raw = _get_raw(...)

```python
raw = _get_raw()
```

### Step 3: Assign picks = _get_picks(...)

```python
picks = _get_picks(raw)
```

### Step 4: Assign ica = ICA(...)

```python
ica = ICA(noise_cov=read_cov(cov_fname), n_components=2)
```

### Step 5: Assign ica.exclude = value

```python
ica.exclude = [0]
```

### Step 6: Assign fig = ica.plot_sources(...)

```python
fig = ica.plot_sources(raw, title='Components')
```

### Step 7: Assign keys = value

```python
keys = ('home', 'home', 'end', 'down', 'up', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'pagedown', 'z', 'z', 's', 's', 'b')
```

### Step 8: Assign x = value

```python
x = fig.mne.traces[0].get_xdata()[0]
```

### Step 9: Assign y = value

```python
y = fig.mne.traces[0].get_ydata()[0]
```

### Step 10: Call fig._fake_click()

```python
fig._fake_click((x, y), xform='data')
```

### Step 11: Call fig._click_ch_name()

```python
fig._click_ch_name(ch_index=0, button=1)
```

### Step 12: Call fig._fake_keypress()

```python
fig._fake_keypress('escape')
```

### Step 13: Call browser_backend._close_all()

```python
browser_backend._close_all()
```

### Step 14: Assign epochs = _get_epochs(...)

```python
epochs = _get_epochs()
```

### Step 15: Assign fig = ica.plot_sources(...)

```python
fig = ica.plot_sources(epochs, title='Components')
```

### Step 16: Assign x = value

```python
x = fig.mne.traces[0].get_xdata()[0]
```

### Step 17: Assign y = value

```python
y = fig.mne.traces[0].get_ydata()[0]
```

### Step 18: Call fig._fake_click()

```python
fig._fake_click((x, y), xform='data')
```

### Step 19: Call fig._click_ch_name()

```python
fig._click_ch_name(ch_index=0, button=1)
```

### Step 20: Call fig._fake_keypress()

```python
fig._fake_keypress('escape')
```

### Step 21: Call ica.fit()

```python
ica.fit(raw, picks=picks)
```

### Step 22: Call fig._fake_keypress()

```python
fig._fake_keypress(key)
```

### Step 23: Call fig._fake_keypress()

```python
fig._fake_keypress(key)
```


## Complete Example

```python
# Setup
# Fixtures: browser_backend

# Workflow
'Test plotting of components as instances of raw and epochs.'
raw = _get_raw()
picks = _get_picks(raw)
ica = ICA(noise_cov=read_cov(cov_fname), n_components=2)
with pytest.warns(RuntimeWarning, match='projection'):
    ica.fit(raw, picks=picks)
ica.exclude = [0]
fig = ica.plot_sources(raw, title='Components')
keys = ('home', 'home', 'end', 'down', 'up', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'pagedown', 'z', 'z', 's', 's', 'b')
for key in keys:
    fig._fake_keypress(key)
x = fig.mne.traces[0].get_xdata()[0]
y = fig.mne.traces[0].get_ydata()[0]
fig._fake_click((x, y), xform='data')
fig._click_ch_name(ch_index=0, button=1)
fig._fake_keypress('escape')
browser_backend._close_all()
epochs = _get_epochs()
fig = ica.plot_sources(epochs, title='Components')
for key in keys:
    fig._fake_keypress(key)
x = fig.mne.traces[0].get_xdata()[0]
y = fig.mne.traces[0].get_ydata()[0]
fig._fake_click((x, y), xform='data')
fig._click_ch_name(ch_index=0, button=1)
fig._fake_keypress('escape')
```

## Next Steps


---

*Source: test_ica.py:559 | Complexity: Advanced | Last updated: 2026-05-18*