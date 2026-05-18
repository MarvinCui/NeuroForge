# How To: Brain Screenshot

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test time viewer screenshot.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `platform`
- `contextlib`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `matplotlib`
- `matplotlib.lines`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.utils`
- `mne.viz`
- `mne.viz._brain`
- `mne.viz._brain.colormap`
- `mne.viz.utils`
- `mne.viz._brain`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, brain_gc
```

## Step-by-Step Guide

### Step 1: 'Test time viewer screenshot.'

```python
'Test time viewer screenshot.'
```

**Verification:**
```python
assert img_nv.shape == want
```

### Step 2: Assign unknown = tiny(...)

```python
tiny_brain, ratio = tiny(tmp_path)
```

**Verification:**
```python
assert img_v.shape[1:] == want[1:]
```

### Step 3: Assign img_nv = tiny_brain.screenshot(...)

```python
img_nv = tiny_brain.screenshot(time_viewer=False)
```

**Verification:**
```python
assert_allclose(img_v.shape[0], want[0] * 4 / 3, atol=3)
```

### Step 4: Assign want = value

```python
want = (_TINY_SIZE[1] * ratio, _TINY_SIZE[0] * ratio, 3)
```

**Verification:**
```python
assert img_nv.shape == want
```

### Step 5: Assign img_v = tiny_brain.screenshot(...)

```python
img_v = tiny_brain.screenshot(time_viewer=True)
```

**Verification:**
```python
assert img_v.shape[1:] == want[1:]
```

### Step 6: Call assert_allclose()

```python
assert_allclose(img_v.shape[0], want[0] * 4 / 3, atol=3)
```

### Step 7: Call tiny_brain.close()

```python
tiny_brain.close()
```


## Complete Example

```python
# Setup
# Fixtures: renderer_interactive_pyvistaqt, tmp_path, brain_gc

# Workflow
'Test time viewer screenshot.'
tiny_brain, ratio = tiny(tmp_path)
img_nv = tiny_brain.screenshot(time_viewer=False)
want = (_TINY_SIZE[1] * ratio, _TINY_SIZE[0] * ratio, 3)
assert img_nv.shape == want
img_v = tiny_brain.screenshot(time_viewer=True)
assert img_v.shape[1:] == want[1:]
assert_allclose(img_v.shape[0], want[0] * 4 / 3, atol=3)
tiny_brain.close()
```

## Next Steps


---

*Source: test_brain.py:877 | Complexity: Intermediate | Last updated: 2026-05-18*