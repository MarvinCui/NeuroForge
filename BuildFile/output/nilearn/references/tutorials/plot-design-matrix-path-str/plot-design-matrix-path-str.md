# How To: Plot Design Matrix Path Str

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test plot_design_matrix directly from file.

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
# Fixtures: tmp_path, suffix, sep
```

## Step-by-Step Guide

### Step 1: 'Test plot_design_matrix directly from file.'

```python
'Test plot_design_matrix directly from file.'
```

**Verification:**
```python
assert ax is not None
```

### Step 2: Assign frame_times = np.linspace(...)

```python
frame_times = np.linspace(0, 127 * 1.0, 128)
```

**Verification:**
```python
assert ax is not None
```

### Step 3: Assign dmtx = make_first_level_design_matrix(...)

```python
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
```

### Step 4: Assign filename = unknown.with_suffix(...)

```python
filename = (tmp_path / 'tmp').with_suffix(suffix)
```

### Step 5: Call dmtx.to_csv()

```python
dmtx.to_csv(filename, sep=sep, index=False)
```

### Step 6: Assign ax = plot_design_matrix(...)

```python
ax = plot_design_matrix(filename)
```

**Verification:**
```python
assert ax is not None
```

### Step 7: Assign ax = plot_design_matrix(...)

```python
ax = plot_design_matrix(str(filename))
```

**Verification:**
```python
assert ax is not None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, suffix, sep

# Workflow
'Test plot_design_matrix directly from file.'
frame_times = np.linspace(0, 127 * 1.0, 128)
dmtx = make_first_level_design_matrix(frame_times, drift_model='polynomial', drift_order=3)
filename = (tmp_path / 'tmp').with_suffix(suffix)
dmtx.to_csv(filename, sep=sep, index=False)
ax = plot_design_matrix(filename)
assert ax is not None
ax = plot_design_matrix(str(filename))
assert ax is not None
```

## Next Steps


---

*Source: test_matrix_plotting.py:172 | Complexity: Intermediate | Last updated: 2026-05-18*