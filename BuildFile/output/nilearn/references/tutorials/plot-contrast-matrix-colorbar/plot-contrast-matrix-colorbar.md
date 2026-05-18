# How To: Plot Contrast Matrix Colorbar

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_contrast_matrix colorbar.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib`
- `numpy`
- `pandas`
- `pytest`
- `matplotlib`
- `nibabel`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.tests._testing`
- `nilearn.image`
- `nilearn.plotting`
- `nilearn.plotting.displays`
- `nilearn.plotting.image.utils`

**Setup Required:**
```python
# Fixtures: colorbar
```

## Step-by-Step Guide

### Step 1: 'Test plot_contrast_matrix colorbar.'

```python
'Test plot_contrast_matrix colorbar.'
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 127 * 1.0, 128)
```

### Step 3: Assign dmtx = make_first_level_design_matrix(...)

```python
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
```

### Step 4: Assign contrast = np.array(...)

```python
contrast = np.array([[1, 0, 0, 1], [0, -2, 1, 0]])
```

### Step 5: Assign ax = plot_contrast_matrix(...)

```python
ax = plot_contrast_matrix(contrast, dmtx, colorbar=colorbar)
```


## Complete Example

```python
# Setup
# Fixtures: colorbar

# Workflow
'Test plot_contrast_matrix colorbar.'
frame_times = np.linspace(0, 127 * 1.0, 128)
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
contrast = np.array([[1, 0, 0, 1], [0, -2, 1, 0]])
ax = plot_contrast_matrix(contrast, dmtx, colorbar=colorbar)
return ax.get_figure()
```

## Next Steps


---

*Source: test_baseline_comparisons.py:618 | Complexity: Intermediate | Last updated: 2026-05-18*