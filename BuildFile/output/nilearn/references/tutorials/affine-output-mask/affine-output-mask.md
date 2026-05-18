# How To: Affine Output Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test affine output mask

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
# Fixtures: n_subjects
```

## Step-by-Step Guide

### Step 1: Assign unknown = fake_fmri_data(...)

```python
func_img, mask = fake_fmri_data()
```

**Verification:**
```python
assert_array_equal(z_image.affine, mask.affine)
```

### Step 2: Assign model = SecondLevelModel(...)

```python
model = SecondLevelModel(mask_img=mask)
```

### Step 3: Assign Y = value

```python
Y = [func_img] * n_subjects
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

### Step 5: Assign model = model.fit(...)

```python
model = model.fit(Y, design_matrix=X)
```

### Step 6: Assign c1 = value

```python
c1 = np.eye(len(model.design_matrix_.columns))[0]
```

### Step 7: Assign z_image = model.compute_contrast(...)

```python
z_image = model.compute_contrast(c1, output_type='z_score')
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(z_image.affine, mask.affine)
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
func_img, mask = fake_fmri_data()
model = SecondLevelModel(mask_img=mask)
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
model = model.fit(Y, design_matrix=X)
c1 = np.eye(len(model.design_matrix_.columns))[0]
z_image = model.compute_contrast(c1, output_type='z_score')
assert_array_equal(z_image.affine, mask.affine)
```

## Next Steps


---

*Source: test_second_level.py:477 | Complexity: Advanced | Last updated: 2026-05-18*