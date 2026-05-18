# How To: Notebook Button Counts

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test button counts.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `mne.datasets`
- `pytest`
- `mne`
- `tempfile`
- `time`
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `pytest`
- `ipywidgets`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `ipywidgets`
- `mne`

**Setup Required:**
```python
# Fixtures: renderer_notebook, brain_gc, nbexec
```

## Step-by-Step Guide

### Step 1: 'Test button counts.'

```python
'Test button counts.'
```

**Verification:**
```python
assert fig.display is None
```

### Step 2: Call mne.viz.set_3d_backend()

```python
mne.viz.set_3d_backend('notebook')
```

**Verification:**
```python
assert number_of_buttons == total_number_of_buttons
```

### Step 3: Assign rend = mne.viz.create_3d_figure(...)

```python
rend = mne.viz.create_3d_figure(size=(100, 100), scene=False)
```

**Verification:**
```python
assert fig.display is not None
```

### Step 4: Assign fig = rend.scene(...)

```python
fig = rend.scene()
```

### Step 5: Call mne.viz.set_3d_title()

```python
mne.viz.set_3d_title(fig, 'Notebook testing')
```

### Step 6: Call mne.viz.set_3d_view()

```python
mne.viz.set_3d_view(fig, 200, 70, focalpoint=[0, 0, 0])
```

**Verification:**
```python
assert fig.display is None
```

### Step 7: Call rend.show()

```python
rend.show()
```

### Step 8: Assign total_number_of_buttons = sum(...)

```python
total_number_of_buttons = sum(('_field' not in k for k in rend.actions.keys()))
```

### Step 9: Assign number_of_buttons = 0

```python
number_of_buttons = 0
```

**Verification:**
```python
assert number_of_buttons == total_number_of_buttons
```

### Step 10: Assign widget = value

```python
widget = action._action
```

### Step 11: Call widget.click()

```python
widget.click()
```


## Complete Example

```python
# Setup
# Fixtures: renderer_notebook, brain_gc, nbexec

# Workflow
'Test button counts.'
from ipywidgets import Button
import mne
mne.viz.set_3d_backend('notebook')
rend = mne.viz.create_3d_figure(size=(100, 100), scene=False)
fig = rend.scene()
mne.viz.set_3d_title(fig, 'Notebook testing')
mne.viz.set_3d_view(fig, 200, 70, focalpoint=[0, 0, 0])
assert fig.display is None
rend.show()
total_number_of_buttons = sum(('_field' not in k for k in rend.actions.keys()))
number_of_buttons = 0
for action in rend.actions.values():
    widget = action._action
    if isinstance(widget, Button):
        widget.click()
        number_of_buttons += 1
assert number_of_buttons == total_number_of_buttons
assert fig.display is not None
```

## Next Steps


---

*Source: test_notebook.py:134 | Complexity: Advanced | Last updated: 2026-05-18*