# How To: Glass Brain Axes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests for class ``GlassBrainAxes``.

## Prerequisites

**Required Modules:**
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn.conftest`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays._slicers`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays`
- `nilearn.plotting.displays._utils`


## Step-by-Step Guide

### Step 1: 'Tests for class ``GlassBrainAxes``.'

```python
'Tests for class ``GlassBrainAxes``.'
```

### Step 2: Assign ax = plt.subplot(...)

```python
ax = plt.subplot(111)
```

### Step 3: Assign axes = GlassBrainAxes(...)

```python
axes = GlassBrainAxes(ax, 'r', 2)
```

### Step 4: Call axes._add_markers()

```python
axes._add_markers(np.array([[0, 0, 0]]), 'g', [10])
```

### Step 5: Assign line_coords = value

```python
line_coords = [np.array([[0, 0, 0], [1, 1, 1]])]
```

### Step 6: Assign line_values = np.array(...)

```python
line_values = np.array([1, 0, 6])
```

### Step 7: Call axes._add_lines()

```python
axes._add_lines(line_coords, line_values, None, vmin=None, vmax=10)
```

### Step 8: Call axes._add_lines()

```python
axes._add_lines(line_coords, line_values, None, vmin=-10, vmax=None)
```

### Step 9: Call axes._add_lines()

```python
axes._add_lines(line_coords, line_values, None, vmin=-10, vmax=-5)
```

### Step 10: Call axes._add_lines()

```python
axes._add_lines(line_coords, line_values, None, vmin=None, vmax=-10)
```

### Step 11: Call axes._add_lines()

```python
axes._add_lines(line_coords, line_values, None, vmin=10, vmax=None)
```


## Complete Example

```python
# Workflow
'Tests for class ``GlassBrainAxes``.'
from nilearn.plotting.displays import GlassBrainAxes
ax = plt.subplot(111)
axes = GlassBrainAxes(ax, 'r', 2)
axes._add_markers(np.array([[0, 0, 0]]), 'g', [10])
line_coords = [np.array([[0, 0, 0], [1, 1, 1]])]
line_values = np.array([1, 0, 6])
with pytest.raises(ValueError, match='If vmax is set to a non-positive number '):
    axes._add_lines(line_coords, line_values, None, vmin=None, vmax=-10)
axes._add_lines(line_coords, line_values, None, vmin=None, vmax=10)
with pytest.raises(ValueError, match='If vmin is set to a non-negative number '):
    axes._add_lines(line_coords, line_values, None, vmin=10, vmax=None)
axes._add_lines(line_coords, line_values, None, vmin=-10, vmax=None)
axes._add_lines(line_coords, line_values, None, vmin=-10, vmax=-5)
```

## Next Steps


---

*Source: test_displays.py:112 | Complexity: Advanced | Last updated: 2026-05-18*