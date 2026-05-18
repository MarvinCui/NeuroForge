# How To: Show Contrast Matrix Axes

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test poassing axes to plot_contrast_matrix.

## Prerequisites

**Required Modules:**
- `itertools`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.tests._testing`
- `nilearn.plotting.matrix._utils`
- `nilearn.plotting.matrix.matrix_plotting`


## Step-by-Step Guide

### Step 1: 'Test poassing axes to plot_contrast_matrix.'

```python
'Test poassing axes to plot_contrast_matrix.'
```

**Verification:**
```python
assert 'constrained' in fig.get_layout_engine().__class__.__name__.lower()
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 127 * 1.0, 128)
```

### Step 3: Assign dmtx = make_first_level_design_matrix(...)

```python
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
```

### Step 4: Assign contrast = np.ones(...)

```python
contrast = np.ones(4)
```

### Step 5: Assign unknown = plt.subplots(...)

```python
fig, ax = plt.subplots(layout='constrained')
```

### Step 6: Call plot_contrast_matrix()

```python
plot_contrast_matrix(contrast, dmtx, axes=ax)
```

**Verification:**
```python
assert 'constrained' in fig.get_layout_engine().__class__.__name__.lower()
```


## Complete Example

```python
# Workflow
'Test poassing axes to plot_contrast_matrix.'
frame_times = np.linspace(0, 127 * 1.0, 128)
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
contrast = np.ones(4)
fig, ax = plt.subplots(layout='constrained')
plot_contrast_matrix(contrast, dmtx, axes=ax)
assert 'constrained' in fig.get_layout_engine().__class__.__name__.lower()
```

## Next Steps


---

*Source: test_matrix_plotting.py:306 | Complexity: Intermediate | Last updated: 2026-05-18*