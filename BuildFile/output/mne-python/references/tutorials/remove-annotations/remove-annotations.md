# How To: Remove Annotations

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that right-click doesn't remove hidden annotation spans.

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
# Fixtures: raw, hide_which, browser_backend
```

## Step-by-Step Guide

### Step 1: "Test that right-click doesn't remove hidden annotation spans."

```python
"Test that right-click doesn't remove hidden annotation spans."
```

**Verification:**
```python
assert len(raw.annotations) == 2
```

### Step 2: Assign descriptions = value

```python
descriptions = ['foo', 'bar']
```

**Verification:**
```python
assert len(raw.annotations) == len(hide_which)
```

### Step 3: Assign ann = Annotations(...)

```python
ann = Annotations(onset=[2, 1], duration=[1, 3], description=descriptions)
```

### Step 4: Call raw.set_annotations()

```python
raw.set_annotations(ann)
```

**Verification:**
```python
assert len(raw.annotations) == 2
```

### Step 5: Assign fig = raw.plot(...)

```python
fig = raw.plot()
```

### Step 6: Call fig._fake_keypress()

```python
fig._fake_keypress('a')
```

**Verification:**
```python
assert len(raw.annotations) == len(hide_which)
```

### Step 7: Assign checkboxes = value

```python
checkboxes = fig.mne.show_hide_annotation_checkboxes
```

### Step 8: Call fig._update_regions_visible()

```python
fig._update_regions_visible()
```

### Step 9: Call fig._fake_click()

```python
fig._fake_click((2.5, 0.1), xform='data', button=3)
```

### Step 10: Call checkboxes.set_active()

```python
checkboxes.set_active(which)
```

### Step 11: Assign hide_key = value

```python
hide_key = descriptions[hide_idx]
```

### Step 12: Assign unknown = False

```python
fig.mne.visible_annotations[hide_key] = False
```


## Complete Example

```python
# Setup
# Fixtures: raw, hide_which, browser_backend

# Workflow
"Test that right-click doesn't remove hidden annotation spans."
descriptions = ['foo', 'bar']
ann = Annotations(onset=[2, 1], duration=[1, 3], description=descriptions)
raw.set_annotations(ann)
assert len(raw.annotations) == 2
fig = raw.plot()
fig._fake_keypress('a')
if browser_backend.name == 'matplotlib':
    checkboxes = fig.mne.show_hide_annotation_checkboxes
    for which in hide_which:
        checkboxes.set_active(which)
else:
    for hide_idx in hide_which:
        hide_key = descriptions[hide_idx]
        fig.mne.visible_annotations[hide_key] = False
    fig._update_regions_visible()
for _ in descriptions:
    fig._fake_click((2.5, 0.1), xform='data', button=3)
assert len(raw.annotations) == len(hide_which)
```

## Next Steps


---

*Source: test_raw.py:964 | Complexity: Advanced | Last updated: 2026-05-18*