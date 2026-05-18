# How To: Plot Img On Surf

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate plot_img_on_surf: test plot img on surf

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
# Fixtures: bg_on_data, symmetric_cmap, colorbar, title
```

## Step-by-Step Guide

### Step 1: Assign unknown = plot_img_on_surf(...)

```python
fig, _ = plot_img_on_surf(stat_map=stat_img, views=['lateral', 'medial', 'dorsal', 'ventral', 'anterior', 'posterior'], hemispheres=['left', 'right'], bg_on_data=bg_on_data, symmetric_cmap=symmetric_cmap, colorbar=colorbar, title=title)
```


## Complete Example

```python
# Setup
# Fixtures: bg_on_data, symmetric_cmap, colorbar, title

# Workflow
fig, _ = plot_img_on_surf(stat_map=stat_img, views=['lateral', 'medial', 'dorsal', 'ventral', 'anterior', 'posterior'], hemispheres=['left', 'right'], bg_on_data=bg_on_data, symmetric_cmap=symmetric_cmap, colorbar=colorbar, title=title)
```

## Next Steps


---

*Source: test_baseline_comparisons.py:469 | Complexity: Beginner | Last updated: 2026-05-18*