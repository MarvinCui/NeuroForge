# How To: Fmri Inputs Flms

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test second level model with first level model as inputs.

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
# Fixtures: rng, confounds, shape_4d_default
```

## Step-by-Step Guide

### Step 1: 'Test second level model with first level model as inputs.'

```python
'Test second level model with first level model as inputs.'
```

### Step 2: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design([shape_4d_default], rk=1)
```

### Step 3: Assign flm = FirstLevelModel.fit(...)

```python
flm = FirstLevelModel(subject_label='01').fit(fmri_data, design_matrices=design_matrices)
```

### Step 4: Assign unknown = value

```python
p, q = (80, 10)
```

### Step 5: Assign X = rng.standard_normal(...)

```python
X = rng.standard_normal(size=(p, q))
```

### Step 6: Assign design_matrix = pd.DataFrame(...)

```python
design_matrix = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
```

### Step 7: Assign flms = value

```python
flms = [flm, flm, flm]
```

### Step 8: Call SecondLevelModel.fit()

```python
SecondLevelModel(mask_img=mask).fit(flms)
```

### Step 9: Call SecondLevelModel.fit()

```python
SecondLevelModel().fit(flms)
```

### Step 10: Call SecondLevelModel.fit()

```python
SecondLevelModel().fit(flms, confounds)
```

### Step 11: Call SecondLevelModel.fit()

```python
SecondLevelModel().fit(flms, confounds, design_matrix)
```


## Complete Example

```python
# Setup
# Fixtures: rng, confounds, shape_4d_default

# Workflow
'Test second level model with first level model as inputs.'
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design([shape_4d_default], rk=1)
flm = FirstLevelModel(subject_label='01').fit(fmri_data, design_matrices=design_matrices)
p, q = (80, 10)
X = rng.standard_normal(size=(p, q))
design_matrix = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
flms = [flm, flm, flm]
SecondLevelModel(mask_img=mask).fit(flms)
SecondLevelModel().fit(flms)
SecondLevelModel().fit(flms, confounds)
SecondLevelModel().fit(flms, confounds, design_matrix)
```

## Next Steps


---

*Source: test_second_level.py:552 | Complexity: Advanced | Last updated: 2026-05-18*