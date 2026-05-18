# How To: Overlay Opacity Bad Shape

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate _Overlay: Test that invalid per-vertex opacity raises.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.viz._3d_overlay`


## Step-by-Step Guide

### Step 1: Assign overlay = _Overlay(...)

```python
overlay = _Overlay(scalars=np.linspace(0, 1, 4), colormap='viridis', rng=(0.0, 1.0), opacity=np.array([0.1, 0.2, 0.3]), name='test')
```


## Complete Example

```python
# Workflow
overlay = _Overlay(scalars=np.linspace(0, 1, 4), colormap='viridis', rng=(0.0, 1.0), opacity=np.array([0.1, 0.2, 0.3]), name='test')
```

## Next Steps


---

*Source: test_3d_overlay.py:28 | Complexity: Beginner | Last updated: 2026-05-18*