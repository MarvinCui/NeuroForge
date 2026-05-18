# How To: Concatenate Images

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that concat with arbitrary sizes works.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `cycler`
- `matplotlib`
- `numpy.testing`
- `mne`
- `mne.epochs`
- `mne.event`
- `mne.io`
- `mne.viz`
- `mne.viz.ui_events`
- `mne.viz.utils`

**Setup Required:**
```python
# Fixtures: a_w, a_h, b_w, b_h, axis
```

## Step-by-Step Guide

### Step 1: 'Test that concat with arbitrary sizes works.'

```python
'Test that concat with arbitrary sizes works.'
```

**Verification:**
```python
assert img.shape == want_shape
```

### Step 2: Assign a = np.zeros(...)

```python
a = np.zeros((a_h, a_w, 3))
```

### Step 3: Assign b = np.zeros(...)

```python
b = np.zeros((b_h, b_w, 3))
```

### Step 4: Assign img = concatenate_images(...)

```python
img = concatenate_images([a, b], axis=axis)
```

**Verification:**
```python
assert img.shape == want_shape
```

### Step 5: Assign want_shape = value

```python
want_shape = (a_h + b_h, max(a_w, b_w), 3)
```

### Step 6: Assign want_shape = value

```python
want_shape = (max(a_h, b_h), a_w + b_w, 3)
```


## Complete Example

```python
# Setup
# Fixtures: a_w, a_h, b_w, b_h, axis

# Workflow
'Test that concat with arbitrary sizes works.'
a = np.zeros((a_h, a_w, 3))
b = np.zeros((b_h, b_w, 3))
img = concatenate_images([a, b], axis=axis)
if axis == 0:
    want_shape = (a_h + b_h, max(a_w, b_w), 3)
else:
    want_shape = (max(a_h, b_h), a_w + b_w, 3)
assert img.shape == want_shape
```

## Next Steps


---

*Source: test_utils.py:212 | Complexity: Intermediate | Last updated: 2026-05-18*