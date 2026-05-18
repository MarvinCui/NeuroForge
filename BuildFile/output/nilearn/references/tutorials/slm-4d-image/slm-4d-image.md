# How To: Slm 4D Image

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Compute contrast with 4D images as input.

See https://github.com/nilearn/nilearn/issues/3058

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`
- `conftest`

**Setup Required:**
```python
# Fixtures: img_4d_mni
```

## Step-by-Step Guide

### Step 1: 'Compute contrast with 4D images as input.\n\n    See https://github.com/nilearn/nilearn/issues/3058\n    '

```python
'Compute contrast with 4D images as input.\n\n    See https://github.com/nilearn/nilearn/issues/3058\n    '
```

### Step 2: Assign model = SecondLevelModel(...)

```python
model = SecondLevelModel()
```

### Step 3: Assign Y = img_4d_mni

```python
Y = img_4d_mni
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * img_4d_mni.shape[3], columns=['intercept'])
```

### Step 5: Assign model = model.fit(...)

```python
model = model.fit(Y, design_matrix=X)
```

### Step 6: Assign c1 = value

```python
c1 = np.eye(len(model.design_matrix_.columns))[0]
```

### Step 7: Call model.compute_contrast()

```python
model.compute_contrast(c1, output_type='z_score')
```


## Complete Example

```python
# Setup
# Fixtures: img_4d_mni

# Workflow
'Compute contrast with 4D images as input.\n\n    See https://github.com/nilearn/nilearn/issues/3058\n    '
model = SecondLevelModel()
Y = img_4d_mni
X = pd.DataFrame([[1]] * img_4d_mni.shape[3], columns=['intercept'])
model = model.fit(Y, design_matrix=X)
c1 = np.eye(len(model.design_matrix_.columns))[0]
model.compute_contrast(c1, output_type='z_score')
```

## Next Steps


---

*Source: test_second_level.py:518 | Complexity: Intermediate | Last updated: 2026-05-18*