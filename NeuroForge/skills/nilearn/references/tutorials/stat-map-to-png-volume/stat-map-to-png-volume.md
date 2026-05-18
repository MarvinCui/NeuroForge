# How To: Stat Map To Png Volume

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check figures plotting for GLM report.

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
# Fixtures: plot_type, height_control, two_sided, threshold, cluster_threshold
```

## Step-by-Step Guide

### Step 1: 'Check figures plotting for GLM report.'

```python
'Check figures plotting for GLM report.'
```

### Step 2: Assign alpha = 0.001

```python
alpha = 0.001
```

### Step 3: Assign table_details = OrderedDict(...)

```python
table_details = OrderedDict()
```

### Step 4: Call table_details.update()

```python
table_details.update({'Threshold Z': np.around(threshold, 3)})
```

### Step 5: Call table_details.update()

```python
table_details.update({'two_sided': two_sided})
```

### Step 6: Call table_details.update()

```python
table_details.update({'cluster_threshold': cluster_threshold})
```

### Step 7: Call table_details.update()

```python
table_details.update({'plot_type': plot_type})
```

### Step 8: Call table_details.update()

```python
table_details.update({'height_control': height_control})
```

### Step 9: Assign table_details = pd.DataFrame.from_dict(...)

```python
table_details = pd.DataFrame.from_dict(table_details, orient='index')
```

### Step 10: Assign unknown = _stat_map_to_png(...)

```python
_, fig = _stat_map_to_png(stat_img=thresholded_img, threshold=threshold, bg_img=load_mni152_template(), cut_coords=None, display_mode='ortho', plot_type=plot_type, table_details=table_details, two_sided=two_sided)
```

### Step 11: Assign unknown = threshold_stats_img(...)

```python
thresholded_img, threshold = threshold_stats_img(stat_img=load_sample_motor_activation_image(), threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
```

### Step 12: Assign unknown = threshold_stats_img(...)

```python
thresholded_img, threshold = threshold_stats_img(stat_img=load_sample_motor_activation_image(), threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
```


## Complete Example

```python
# Setup
# Fixtures: plot_type, height_control, two_sided, threshold, cluster_threshold

# Workflow
'Check figures plotting for GLM report.'
alpha = 0.001
if height_control is None and threshold == 3:
    with pytest.warns(FutureWarning, match="nilearn version>=0.15, the default 'threshold' will be set"):
        thresholded_img, threshold = threshold_stats_img(stat_img=load_sample_motor_activation_image(), threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
else:
    thresholded_img, threshold = threshold_stats_img(stat_img=load_sample_motor_activation_image(), threshold=threshold, alpha=alpha, cluster_threshold=cluster_threshold, height_control=height_control, two_sided=two_sided)
table_details = OrderedDict()
table_details.update({'Threshold Z': np.around(threshold, 3)})
table_details.update({'two_sided': two_sided})
table_details.update({'cluster_threshold': cluster_threshold})
table_details.update({'plot_type': plot_type})
table_details.update({'height_control': height_control})
table_details = pd.DataFrame.from_dict(table_details, orient='index')
_, fig = _stat_map_to_png(stat_img=thresholded_img, threshold=threshold, bg_img=load_mni152_template(), cut_coords=None, display_mode='ortho', plot_type=plot_type, table_details=table_details, two_sided=two_sided)
return fig
```

## Next Steps


---

*Source: test_baseline_comparisons.py:39 | Complexity: Advanced | Last updated: 2026-05-18*