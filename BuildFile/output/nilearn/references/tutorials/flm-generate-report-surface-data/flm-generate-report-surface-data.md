# How To: Flm Generate Report Surface Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Generate report from flm fitted surface.

Need a larger image to avoid issues with colormap.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level`
- `nilearn.maskers`
- `nilearn.reporting`
- `nilearn.reporting.tests._testing`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Generate report from flm fitted surface.\n\n    Need a larger image to avoid issues with colormap.\n    '

```python
'Generate report from flm fitted surface.\n\n    Need a larger image to avoid issues with colormap.\n    '
```

### Step 2: Assign t_r = 2.0

```python
t_r = 2.0
```

### Step 3: Assign events = basic_paradigm(...)

```python
events = basic_paradigm()
```

### Step 4: Assign n_scans = 10

```python
n_scans = 10
```

### Step 5: Assign mesh = value

```python
mesh = load_fsaverage(mesh='fsaverage5')['pial']
```

### Step 6: Assign data = value

```python
data = {}
```

### Step 7: Assign fmri_data = SurfaceImage(...)

```python
fmri_data = SurfaceImage(mesh, data)
```

### Step 8: Assign model = FirstLevelModel(...)

```python
model = FirstLevelModel(t_r=t_r, smoothing_fwhm=None, standardize=None, minimize_memory=False)
```

### Step 9: Call model.fit()

```python
model.fit(fmri_data, events=events)
```

### Step 10: Call generate_and_check_glm_report()

```python
generate_and_check_glm_report(model, contrasts='c0', extra_warnings_allowed=True)
```

### Step 11: Assign data_shape = value

```python
data_shape = (val.n_vertices, n_scans)
```

### Step 12: Assign data_part = rng.normal(...)

```python
data_part = rng.normal(size=data_shape)
```

### Step 13: Assign unknown = data_part

```python
data[key] = data_part
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Generate report from flm fitted surface.\n\n    Need a larger image to avoid issues with colormap.\n    '
t_r = 2.0
events = basic_paradigm()
n_scans = 10
mesh = load_fsaverage(mesh='fsaverage5')['pial']
data = {}
for key, val in mesh.parts.items():
    data_shape = (val.n_vertices, n_scans)
    data_part = rng.normal(size=data_shape)
    data[key] = data_part
fmri_data = SurfaceImage(mesh, data)
model = FirstLevelModel(t_r=t_r, smoothing_fwhm=None, standardize=None, minimize_memory=False)
model.fit(fmri_data, events=events)
generate_and_check_glm_report(model, contrasts='c0', extra_warnings_allowed=True)
```

## Next Steps


---

*Source: test_glm_reporter.py:519 | Complexity: Advanced | Last updated: 2026-05-18*