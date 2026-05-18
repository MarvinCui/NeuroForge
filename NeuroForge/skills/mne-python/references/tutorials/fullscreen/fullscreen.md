# How To: Fullscreen

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test fullscreen mode.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `contextlib`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.coreg`
- `mne.datasets`
- `mne.io`
- `mne.utils`
- `mne.viz`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `mne.gui`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.gui`
- `mne.gui`
- `mne.gui`

**Setup Required:**
```python
# Fixtures: renderer_interactive_pyvistaqt
```

## Step-by-Step Guide

### Step 1: 'Test fullscreen mode.'

```python
'Test fullscreen mode.'
```

### Step 2: Assign coreg = coregistration(...)

```python
coreg = coregistration(subject='sample', subjects_dir=subjects_dir, fullscreen=True)
```

### Step 3: Assign coreg._accept_close_event = True

```python
coreg._accept_close_event = True
```

### Step 4: Call coreg.close()

```python
coreg.close()
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt

# Workflow
'Test fullscreen mode.'
from mne.gui import coregistration
coreg = coregistration(subject='sample', subjects_dir=subjects_dir, fullscreen=True)
coreg._accept_close_event = True
coreg.close()
```

## Next Steps


---

*Source: test_coreg.py:310 | Complexity: Intermediate | Last updated: 2026-05-18*