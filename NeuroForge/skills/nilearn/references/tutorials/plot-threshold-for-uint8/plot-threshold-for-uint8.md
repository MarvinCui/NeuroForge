# How To: Plot Threshold For Uint8

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Mask was applied in [-threshold, threshold] which is problematic        for uint8 data.

See https://github.com/nilearn/nilearn/issues/611 for more details.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`
- `nilearn.plotting`
- `nilearn.plotting.image.utils`

**Setup Required:**
```python
# Fixtures: affine_eye, plot_func
```

## Step-by-Step Guide

### Step 1: 'Mask was applied in [-threshold, threshold] which is problematic        for uint8 data.\n\n    See https://github.com/nilearn/nilearn/issues/611 for more details.\n    '

```python
'Mask was applied in [-threshold, threshold] which is problematic        for uint8 data.\n\n    See https://github.com/nilearn/nilearn/issues/611 for more details.\n    '
```

**Verification:**
```python
assert plotted_array.mask.sum() == 1
```

### Step 2: Assign data = value

```python
data = 10 * np.ones((10, 10, 10), dtype='uint8')
```

**Verification:**
```python
assert plotted_array.mask[-1, 0]
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(data, affine_eye)
```

### Step 4: Assign threshold = 5

```python
threshold = 5
```

### Step 5: Assign kwargs = value

```python
kwargs = {'threshold': threshold, 'display_mode': 'z'}
```

### Step 6: Assign display = plot_func(...)

```python
display = plot_func(img, colorbar=True, **kwargs)
```

### Step 7: Assign ax = value

```python
ax = next(iter(display.axes.values())).ax
```

### Step 8: Assign plotted_array = unknown.get_array(...)

```python
plotted_array = ax.images[0].get_array()
```

**Verification:**
```python
assert plotted_array.mask.sum() == 1
```

### Step 9: Call plt.close()

```python
plt.close()
```

### Step 10: Assign unknown = 0

```python
data[0, 0, 0] = 0
```

### Step 11: Assign unknown = 0

```python
data[0, 0] = 0
```

### Step 12: Assign unknown = None

```python
kwargs['bg_img'] = None
```

### Step 13: Assign unknown = value

```python
kwargs['cut_coords'] = [0]
```


## Complete Example

```python
# Setup
# Fixtures: affine_eye, plot_func

# Workflow
'Mask was applied in [-threshold, threshold] which is problematic        for uint8 data.\n\n    See https://github.com/nilearn/nilearn/issues/611 for more details.\n    '
data = 10 * np.ones((10, 10, 10), dtype='uint8')
if plot_func is plot_stat_map:
    data[0, 0, 0] = 0
else:
    data[0, 0] = 0
img = Nifti1Image(data, affine_eye)
threshold = 5
kwargs = {'threshold': threshold, 'display_mode': 'z'}
if plot_func is plot_stat_map:
    kwargs['bg_img'] = None
    kwargs['cut_coords'] = [0]
display = plot_func(img, colorbar=True, **kwargs)
ax = next(iter(display.axes.values())).ax
plotted_array = ax.images[0].get_array()
assert plotted_array.mask.sum() == 1
assert plotted_array.mask[-1, 0]
plt.close()
```

## Next Steps


---

*Source: test_img_plotting.py:123 | Complexity: Advanced | Last updated: 2026-05-18*