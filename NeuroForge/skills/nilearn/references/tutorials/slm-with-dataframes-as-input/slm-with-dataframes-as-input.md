# How To: Slm With Dataframes As Input

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test second level reporting when input is a dataframe.

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
# Fixtures: tmp_path, shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'Test second level reporting when input is a dataframe.'

```python
'Test second level reporting when input is a dataframe.'
```

### Step 2: Assign file_path = write_fake_bold_img(...)

```python
file_path = write_fake_bold_img(file_path=tmp_path / 'img.nii.gz', shape=shape_3d_default)
```

### Step 3: Assign dfcols = value

```python
dfcols = ['subject_label', 'map_name', 'effects_map_path']
```

### Step 4: Assign dfrows = value

```python
dfrows = [['01', 'a', file_path], ['02', 'a', file_path], ['03', 'a', file_path]]
```

### Step 5: Assign niidf = pd.DataFrame(...)

```python
niidf = pd.DataFrame(dfrows, columns=dfcols)
```

### Step 6: Assign model = SecondLevelModel.fit(...)

```python
model = SecondLevelModel(minimize_memory=False).fit(niidf)
```

### Step 7: Assign c1 = value

```python
c1 = np.eye(len(model.design_matrix_.columns))[0]
```

### Step 8: Call generate_and_check_glm_report()

```python
generate_and_check_glm_report(model, contrasts=c1, first_level_contrast='a', extra_warnings_allowed=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, shape_3d_default

# Workflow
'Test second level reporting when input is a dataframe.'
file_path = write_fake_bold_img(file_path=tmp_path / 'img.nii.gz', shape=shape_3d_default)
dfcols = ['subject_label', 'map_name', 'effects_map_path']
dfrows = [['01', 'a', file_path], ['02', 'a', file_path], ['03', 'a', file_path]]
niidf = pd.DataFrame(dfrows, columns=dfcols)
model = SecondLevelModel(minimize_memory=False).fit(niidf)
c1 = np.eye(len(model.design_matrix_.columns))[0]
generate_and_check_glm_report(model, contrasts=c1, first_level_contrast='a', extra_warnings_allowed=True)
```

## Next Steps


---

*Source: test_glm_reporter.py:366 | Complexity: Advanced | Last updated: 2026-05-18*