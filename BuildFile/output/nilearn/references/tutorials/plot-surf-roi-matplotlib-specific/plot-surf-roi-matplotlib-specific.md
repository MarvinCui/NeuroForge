# How To: Plot Surf Roi Matplotlib Specific

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi
for matplotlib engine specific parameters.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `tempfile`
- `numpy`
- `pandas`
- `pytest`
- `numpy.testing`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.exceptions`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, surface_image_roi
```

## Step-by-Step Guide

### Step 1: 'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for matplotlib engine specific parameters.\n    '

```python
'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for matplotlib engine specific parameters.\n    '
```

**Verification:**
```python
assert cbar_vmin == 1.0
```

### Step 2: Assign ENGINE = 'matplotlib'

```python
ENGINE = 'matplotlib'
```

**Verification:**
```python
assert cbar_vmax == 8.0
```

### Step 3: Assign img = plot_surf_roi(...)

```python
img = plot_surf_roi(surface_image_roi.mesh, roi_map=surface_image_roi, avg_method='median', cbar_tick_format='%i', vmin=1.2, vmax=8.9, colorbar=True, engine=ENGINE)
```

**Verification:**
```python
assert cbar_vmin == 1.2
```

### Step 4: Call img.canvas.draw()

```python
img.canvas.draw()
```

**Verification:**
```python
assert cbar_vmax == 8.9
```

### Step 5: Assign cbar = value

```python
cbar = img.axes[-1]
```

### Step 6: Assign cbar_vmin = float(...)

```python
cbar_vmin = float(cbar.get_yticklabels()[0].get_text())
```

### Step 7: Assign cbar_vmax = float(...)

```python
cbar_vmax = float(cbar.get_yticklabels()[-1].get_text())
```

**Verification:**
```python
assert cbar_vmin == 1.0
```

### Step 8: Assign img2 = plot_surf_roi(...)

```python
img2 = plot_surf_roi(surface_image_roi.mesh, roi_map=surface_image_roi, vmin=1.2, vmax=8.9, colorbar=True, cbar_tick_format='%.2g', engine=ENGINE)
```

### Step 9: Call img2.canvas.draw()

```python
img2.canvas.draw()
```

### Step 10: Assign cbar = value

```python
cbar = img2.axes[-1]
```

### Step 11: Assign cbar_vmin = float(...)

```python
cbar_vmin = float(cbar.get_yticklabels()[0].get_text())
```

### Step 12: Assign cbar_vmax = float(...)

```python
cbar_vmax = float(cbar.get_yticklabels()[-1].get_text())
```

**Verification:**
```python
assert cbar_vmin == 1.2
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, surface_image_roi

# Workflow
'Test for nilearn.plotting.surface.surf_plotting.plot_surf_roi\n    for matplotlib engine specific parameters.\n    '
ENGINE = 'matplotlib'
img = plot_surf_roi(surface_image_roi.mesh, roi_map=surface_image_roi, avg_method='median', cbar_tick_format='%i', vmin=1.2, vmax=8.9, colorbar=True, engine=ENGINE)
img.canvas.draw()
cbar = img.axes[-1]
cbar_vmin = float(cbar.get_yticklabels()[0].get_text())
cbar_vmax = float(cbar.get_yticklabels()[-1].get_text())
assert cbar_vmin == 1.0
assert cbar_vmax == 8.0
img2 = plot_surf_roi(surface_image_roi.mesh, roi_map=surface_image_roi, vmin=1.2, vmax=8.9, colorbar=True, cbar_tick_format='%.2g', engine=ENGINE)
img2.canvas.draw()
cbar = img2.axes[-1]
cbar_vmin = float(cbar.get_yticklabels()[0].get_text())
cbar_vmax = float(cbar.get_yticklabels()[-1].get_text())
assert cbar_vmin == 1.2
assert cbar_vmax == 8.9
```

## Next Steps


---

*Source: test_surf_plotting.py:940 | Complexity: Advanced | Last updated: 2026-05-18*