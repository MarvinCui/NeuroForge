# How To: Fmri Inputs Images

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test second level model with image as inputs.

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
# Fixtures: rng, shape_3d_default, confounds
```

## Step-by-Step Guide

### Step 1: 'Test second level model with image as inputs.'

```python
'Test second level model with image as inputs.'
```

### Step 2: Assign unknown = value

```python
p, q = (80, 10)
```

### Step 3: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal(size=(p, q))
```

### Step 4: Assign design_matrix = pd.DataFrame(...)

```python
design_matrix = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
```

### Step 5: Assign shape_3d = value

```python
shape_3d = [(*shape_3d_default, 1)]
```

### Step 6: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, _ = generate_fake_fmri_data_and_design(shape_3d)
```

### Step 7: Assign fmri_data = value

```python
fmri_data = fmri_data[0]
```

### Step 8: Assign niimgs = value

```python
niimgs = [fmri_data, fmri_data, fmri_data]
```

### Step 9: Call SecondLevelModel.fit()

```python
SecondLevelModel().fit(niimgs, confounds, design_matrix)
```

### Step 10: Assign niimg_4d = concat_imgs(...)

```python
niimg_4d = concat_imgs(niimgs)
```

### Step 11: Call SecondLevelModel.fit()

```python
SecondLevelModel().fit(niimg_4d, confounds, design_matrix)
```


## Complete Example

```python
# Setup
# Fixtures: rng, shape_3d_default, confounds

# Workflow
'Test second level model with image as inputs.'
p, q = (80, 10)
X = rng.standard_normal(size=(p, q))
design_matrix = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
shape_3d = [(*shape_3d_default, 1)]
_, fmri_data, _ = generate_fake_fmri_data_and_design(shape_3d)
fmri_data = fmri_data[0]
niimgs = [fmri_data, fmri_data, fmri_data]
SecondLevelModel().fit(niimgs, confounds, design_matrix)
niimg_4d = concat_imgs(niimgs)
SecondLevelModel().fit(niimg_4d, confounds, design_matrix)
```

## Next Steps


---

*Source: test_second_level.py:582 | Complexity: Advanced | Last updated: 2026-05-18*