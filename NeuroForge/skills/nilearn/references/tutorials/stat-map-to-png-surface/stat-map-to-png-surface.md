# How To: Stat Map To Png Surface

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check figures plotting for GLM report for surface data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `collections`
- `matplotlib`
- `numpy`
- `pandas`
- `pytest`
- `nilearn.datasets`
- `nilearn.glm._reporting_utils`
- `nilearn.glm.thresholding`

**Setup Required:**
```python
# Fixtures: height_control, two_sided, threshold, cluster_threshold
```

## Step-by-Step Guide

### Step 1: 'Check figures plotting for GLM report for surface data.'

```python
'Check figures plotting for GLM report for surface data.'
```

### Step 2: Assign alpha = 0.05

```python
alpha = 0.05
```

### Step 3: Assign surf_img = load_fsaverage_data(...)

```python
surf_img = load_fsaverage_data(mesh_type='inflated')
```

### Step 4: Assign unknown = threshold_stats_img(...)

```python
thresholded_img, threshold = threshold_stats_img(stat_img=surf_img, threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
```

### Step 5: Assign table_details = OrderedDict(...)

```python
table_details = OrderedDict()
```

### Step 6: Call table_details.update()

```python
table_details.update({'Threshold Z': np.around(threshold, 3)})
```

### Step 7: Call table_details.update()

```python
table_details.update({'two_sided': two_sided})
```

### Step 8: Call table_details.update()

```python
table_details.update({'height_control': height_control})
```

### Step 9: Call table_details.update()

```python
table_details.update({'cluster_threshold': cluster_threshold})
```

### Step 10: Assign table_details = pd.DataFrame.from_dict(...)

```python
table_details = pd.DataFrame.from_dict(table_details, orient='index')
```

### Step 11: Assign unknown = _stat_map_to_png(...)

```python
_, fig = _stat_map_to_png(stat_img=thresholded_img, threshold=threshold, bg_img=surf_img, cut_coords=None, display_mode='ortho', plot_type='slice', table_details=table_details, two_sided=two_sided)
```


## Complete Example

```python
# Setup
# Fixtures: height_control, two_sided, threshold, cluster_threshold

# Workflow
'Check figures plotting for GLM report for surface data.'
alpha = 0.05
surf_img = load_fsaverage_data(mesh_type='inflated')
thresholded_img, threshold = threshold_stats_img(stat_img=surf_img, threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
table_details = OrderedDict()
table_details.update({'Threshold Z': np.around(threshold, 3)})
table_details.update({'two_sided': two_sided})
table_details.update({'height_control': height_control})
table_details.update({'cluster_threshold': cluster_threshold})
table_details = pd.DataFrame.from_dict(table_details, orient='index')
_, fig = _stat_map_to_png(stat_img=thresholded_img, threshold=threshold, bg_img=surf_img, cut_coords=None, display_mode='ortho', plot_type='slice', table_details=table_details, two_sided=two_sided)
return fig
```

## Next Steps


---

*Source: test_baseline_comparisons.py:107 | Complexity: Advanced | Last updated: 2026-05-18*