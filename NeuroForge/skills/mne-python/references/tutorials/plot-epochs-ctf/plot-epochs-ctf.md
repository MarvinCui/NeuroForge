# How To: Plot Epochs Ctf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test of basic CTF plotting.

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
# Fixtures: raw_ctf, browser_backend
```

## Step-by-Step Guide

### Step 1: 'Test of basic CTF plotting.'

```python
'Test of basic CTF plotting.'
```

### Step 2: Call raw_ctf.pick()

```python
raw_ctf.pick(['UDIO001', 'UPPT001', 'SCLK01-177', 'BG1-4304', 'MLC11-4304', 'EEG058', 'UADC007-4302'])
```

### Step 3: Assign evts = make_fixed_length_events(...)

```python
evts = make_fixed_length_events(raw_ctf)
```

### Step 4: Assign epochs = Epochs(...)

```python
epochs = Epochs(raw_ctf, evts, preload=True)
```

### Step 5: Call epochs.plot()

```python
epochs.plot()
```

### Step 6: Call browser_backend._close_all()

```python
browser_backend._close_all()
```

### Step 7: Assign fig = epochs.plot(...)

```python
fig = epochs.plot(butterfly=True)
```

### Step 8: Assign keys = value

```python
keys = ('b', 'b', 'pagedown', 'down', 'up', 'down', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'home', 'end', 'z', 'z', 's', 's', '?', 'h', 'j')
```

### Step 9: Call fig._fake_scroll()

```python
fig._fake_scroll(0.5, 0.5, -0.5)
```

### Step 10: Call fig._fake_scroll()

```python
fig._fake_scroll(0.5, 0.5, 0.5)
```

### Step 11: Call fig._resize_by_factor()

```python
fig._resize_by_factor(1)
```

### Step 12: Call fig._fake_keypress()

```python
fig._fake_keypress('escape')
```

### Step 13: Call fig._fake_keypress()

```python
fig._fake_keypress(key)
```


## Complete Example

```python
# Setup
# Fixtures: raw_ctf, browser_backend

# Workflow
'Test of basic CTF plotting.'
raw_ctf.pick(['UDIO001', 'UPPT001', 'SCLK01-177', 'BG1-4304', 'MLC11-4304', 'EEG058', 'UADC007-4302'])
evts = make_fixed_length_events(raw_ctf)
epochs = Epochs(raw_ctf, evts, preload=True)
epochs.plot()
browser_backend._close_all()
fig = epochs.plot(butterfly=True)
keys = ('b', 'b', 'pagedown', 'down', 'up', 'down', 'right', 'left', '-', '+', '=', 'd', 'd', 'pageup', 'home', 'end', 'z', 'z', 's', 's', '?', 'h', 'j')
for key in keys:
    fig._fake_keypress(key)
fig._fake_scroll(0.5, 0.5, -0.5)
fig._fake_scroll(0.5, 0.5, 0.5)
fig._resize_by_factor(1)
fig._fake_keypress('escape')
```

## Next Steps


---

*Source: test_epochs.py:435 | Complexity: Advanced | Last updated: 2026-05-18*