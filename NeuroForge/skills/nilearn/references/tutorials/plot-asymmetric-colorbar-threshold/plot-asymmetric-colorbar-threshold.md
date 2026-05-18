# How To: Plot Asymmetric Colorbar Threshold

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test plot asymmetric colorbar threshold

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
# Fixtures: tmp_path, plot_func, threshold, expected_ticks
```

## Step-by-Step Guide

### Step 1: Assign img_data = np.zeros(...)

```python
img_data = np.zeros((10, 10, 10))
```

**Verification:**
```python
assert [float(tick.get_text()) for tick in display._cbar.ax.get_yticklabels()] == expected_ticks
```

### Step 2: Assign unknown = 5

```python
img_data[4:6, 2:4, 4:6] = 5
```

### Step 3: Assign unknown = 10

```python
img_data[5:7, 3:7, 3:6] = 10
```

### Step 4: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(img_data, affine=np.eye(4))
```

### Step 5: Assign display = plot_func(...)

```python
display = plot_func(img, threshold=threshold, colorbar=True)
```

### Step 6: Call plt.savefig()

```python
plt.savefig(tmp_path / 'test.png')
```

**Verification:**
```python
assert [float(tick.get_text()) for tick in display._cbar.ax.get_yticklabels()] == expected_ticks
```

### Step 7: Call plt.close()

```python
plt.close()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, plot_func, threshold, expected_ticks

# Workflow
img_data = np.zeros((10, 10, 10))
img_data[4:6, 2:4, 4:6] = 5
img_data[5:7, 3:7, 3:6] = 10
img = Nifti1Image(img_data, affine=np.eye(4))
display = plot_func(img, threshold=threshold, colorbar=True)
plt.savefig(tmp_path / 'test.png')
assert [float(tick.get_text()) for tick in display._cbar.ax.get_yticklabels()] == expected_ticks
plt.close()
```

## Next Steps


---

*Source: test_img_plotting.py:268 | Complexity: Intermediate | Last updated: 2026-05-18*