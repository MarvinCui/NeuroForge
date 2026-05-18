# How To: Overlay Opacity Per Vertex

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate _Overlay: Test per-vertex opacity support in overlay color mapping.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.viz._3d_overlay`


## Step-by-Step Guide

### Step 1: Assign overlay = _Overlay(...)

```python
overlay = _Overlay(scalars=np.linspace(0, 1, n_vertices), colormap='viridis', rng=(0.0, 1.0), opacity=np.array([0.0, 0.25, 0.5, 1.0]), name='test')
```


## Complete Example

```python
# Workflow
overlay = _Overlay(scalars=np.linspace(0, 1, n_vertices), colormap='viridis', rng=(0.0, 1.0), opacity=np.array([0.0, 0.25, 0.5, 1.0]), name='test')
```

## Next Steps


---

*Source: test_3d_overlay.py:15 | Complexity: Beginner | Last updated: 2026-05-18*