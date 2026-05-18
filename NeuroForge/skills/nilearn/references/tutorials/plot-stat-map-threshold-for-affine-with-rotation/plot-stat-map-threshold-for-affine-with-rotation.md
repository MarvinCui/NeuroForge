# How To: Plot Stat Map Threshold For Affine With Rotation

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate array: Tests for plot_stat_map with thresholding and resampling.

Threshold was not being applied when affine has a rotation.
See https://github.com/nilearn/nilearn/issues/599 for more details.

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
- `nilearn.image.resampling`
- `nilearn.plotting`
- `nilearn.plotting.find_cuts`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, rng
```

## Step-by-Step Guide

### Step 1: Assign affine = np.array(...)

```python
affine = np.array([[-3.0, 1.0, 0.0, 1.0], [-1.0, -3.0, 0.0, -2.0], [0.0, 0.0, 3.0, 3.0], [0.0, 0.0, 0.0, 1.0]])
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, rng

# Workflow
affine = np.array([[-3.0, 1.0, 0.0, 1.0], [-1.0, -3.0, 0.0, -2.0], [0.0, 0.0, 3.0, 3.0], [0.0, 0.0, 0.0, 1.0]])
```

## Next Steps


---

*Source: test_plot_stat_map.py:109 | Complexity: Beginner | Last updated: 2026-05-18*