# How To: Plot Noncurrent Axes

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Regression test for Issue #450.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn.image`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, rng
```

## Step-by-Step Guide

### Step 1: 'Regression test for Issue #450.'

```python
'Regression test for Issue #450.'
```

**Verification:**
```python
assert plt.gcf() == fh2, 'fh2 was the last plot created.'
```

### Step 2: Assign maps_img = Nifti1Image(...)

```python
maps_img = Nifti1Image(rng.random((10, 10, 10)), np.eye(4))
```

**Verification:**
```python
assert ax_fh == fh1, f'New axis {ax_name} should be in fh1.'
```

### Step 3: Assign fh1 = plt.figure(...)

```python
fh1 = plt.figure()
```

### Step 4: Assign fh2 = plt.figure(...)

```python
fh2 = plt.figure()
```

### Step 5: Assign ax1 = fh1.add_subplot(...)

```python
ax1 = fh1.add_subplot(1, 1, 1)
```

**Verification:**
```python
assert plt.gcf() == fh2, 'fh2 was the last plot created.'
```

### Step 6: Assign slicer = plot_glass_brain(...)

```python
slicer = plot_glass_brain(maps_img, axes=ax1, title='test')
```

### Step 7: Assign ax_fh = niax.ax.get_figure(...)

```python
ax_fh = niax.ax.get_figure()
```

**Verification:**
```python
assert ax_fh == fh1, f'New axis {ax_name} should be in fh1.'
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, rng

# Workflow
'Regression test for Issue #450.'
maps_img = Nifti1Image(rng.random((10, 10, 10)), np.eye(4))
fh1 = plt.figure()
fh2 = plt.figure()
ax1 = fh1.add_subplot(1, 1, 1)
assert plt.gcf() == fh2, 'fh2 was the last plot created.'
slicer = plot_glass_brain(maps_img, axes=ax1, title='test')
for ax_name, niax in slicer.axes.items():
    ax_fh = niax.ax.get_figure()
    assert ax_fh == fh1, f'New axis {ax_name} should be in fh1.'
```

## Next Steps


---

*Source: test_plot_glass_brain.py:36 | Complexity: Intermediate | Last updated: 2026-05-18*