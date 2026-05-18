# How To: Save Contrast Matrix

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check saving matrices to file.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check saving matrices to file.'

```python
'Check saving matrices to file.'
```

**Verification:**
```python
assert (tmp_path / 'contrast.png').exists()
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 127 * 1.0, 128)
```

**Verification:**
```python
assert ax is None
```

### Step 3: Assign dmtx = make_first_level_design_matrix(...)

```python
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
```

**Verification:**
```python
assert (tmp_path / 'contrast.pdf').exists()
```

### Step 4: Assign contrast = np.ones(...)

```python
contrast = np.ones(4)
```

### Step 5: Assign ax = plot_contrast_matrix(...)

```python
ax = plot_contrast_matrix(contrast, dmtx, output_file=tmp_path / 'contrast.png')
```

**Verification:**
```python
assert (tmp_path / 'contrast.png').exists()
```

### Step 6: Call plot_contrast_matrix()

```python
plot_contrast_matrix(contrast, dmtx, output_file=tmp_path / 'contrast.pdf')
```

**Verification:**
```python
assert (tmp_path / 'contrast.pdf').exists()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check saving matrices to file.'
frame_times = np.linspace(0, 127 * 1.0, 128)
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
contrast = np.ones(4)
ax = plot_contrast_matrix(contrast, dmtx, output_file=tmp_path / 'contrast.png')
assert (tmp_path / 'contrast.png').exists()
assert ax is None
plot_contrast_matrix(contrast, dmtx, output_file=tmp_path / 'contrast.pdf')
assert (tmp_path / 'contrast.pdf').exists()
```

## Next Steps


---

*Source: test_matrix_plotting.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*