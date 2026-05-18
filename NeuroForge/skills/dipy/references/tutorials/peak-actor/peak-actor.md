# How To: Peak Actor

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Fixture to create a Peaks Actor.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `numpy`
- `pytest`
- `dipy.direction.peaks`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.viz.horizon.tab.base`
- `dipy.viz.horizon.tab.peak`
- `dipy.viz.horizon.visualizer.peak`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Fixture to create a Peaks Actor.'

```python
'Fixture to create a Peaks Actor.'
```

### Step 2: Assign peak_dirs = value

```python
peak_dirs = 255 * rng.random((5, 5, 5, 5, 3))
```

### Step 3: Assign pam = PeaksAndMetrics(...)

```python
pam = PeaksAndMetrics()
```

### Step 4: Assign pam.peak_dirs = peak_dirs

```python
pam.peak_dirs = peak_dirs
```

### Step 5: Assign pam.affine = np.eye(...)

```python
pam.affine = np.eye(4)
```

### Step 6: Assign peak_viz = PeaksVisualizer(...)

```python
peak_viz = PeaksVisualizer((pam.peak_dirs, pam.affine), False, 'mock_peaks')
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Fixture to create a Peaks Actor.'
peak_dirs = 255 * rng.random((5, 5, 5, 5, 3))
pam = PeaksAndMetrics()
pam.peak_dirs = peak_dirs
pam.affine = np.eye(4)
peak_viz = PeaksVisualizer((pam.peak_dirs, pam.affine), False, 'mock_peaks')
return peak_viz.actors[0]
```

## Next Steps


---

*Source: test_peak.py:21 | Complexity: Intermediate | Last updated: 2026-05-18*