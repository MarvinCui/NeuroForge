# How To: Explicit Fixed Effects

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the fixed effects performed manually/explicitly.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `string`
- `unittest.mock`
- `warnings`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.cluster`
- `sklearn.utils.estimator_checks`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.first_level.first_level`
- `nilearn.glm.regression`
- `nilearn.glm.thresholding`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'Test the fixed effects performed manually/explicitly.'

```python
'Test the fixed effects performed manually/explicitly.'
```

**Verification:**
```python
assert_almost_equal(get_data(fixed_fx_contrast), get_data(fixed_fx_dic['effect_size']))
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(*shape_3d_default, 4), (*shape_3d_default, 5)], 3)
```

**Verification:**
```python
assert_almost_equal(get_data(fixed_fx_variance), get_data(fixed_fx_dic['effect_variance']))
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
```

**Verification:**
```python
assert_almost_equal(get_data(fixed_fx_stat), get_data(fixed_fx_dic['stat']))
```

### Step 4: Assign contrast = value

```python
contrast = np.eye(rk)[1]
```

### Step 5: Assign multi_run_model = FirstLevelModel.fit(...)

```python
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[:1])
```

### Step 6: Assign dic1 = multi_run_model.compute_contrast(...)

```python
dic1 = multi_run_model.compute_contrast(contrast, output_type='all')
```

### Step 7: Call multi_run_model.fit()

```python
multi_run_model.fit(fmri_data[1], design_matrices=design_matrices[1:])
```

### Step 8: Assign dic2 = multi_run_model.compute_contrast(...)

```python
dic2 = multi_run_model.compute_contrast(contrast, output_type='all')
```

### Step 9: Call multi_run_model.fit()

```python
multi_run_model.fit(fmri_data, design_matrices=design_matrices)
```

### Step 10: Assign fixed_fx_dic = multi_run_model.compute_contrast(...)

```python
fixed_fx_dic = multi_run_model.compute_contrast(contrast, output_type='all')
```

### Step 11: Assign contrasts = value

```python
contrasts = [dic1['effect_size'], dic2['effect_size']]
```

### Step 12: Assign variance = value

```python
variance = [dic1['effect_variance'], dic2['effect_variance']]
```

### Step 13: Assign unknown = compute_fixed_effects(...)

```python
fixed_fx_contrast, fixed_fx_variance, fixed_fx_stat, _ = compute_fixed_effects(contrasts, variance, mask)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(get_data(fixed_fx_contrast), get_data(fixed_fx_dic['effect_size']))
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(get_data(fixed_fx_variance), get_data(fixed_fx_dic['effect_variance']))
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(get_data(fixed_fx_stat), get_data(fixed_fx_dic['stat']))
```

### Step 17: Call compute_fixed_effects()

```python
compute_fixed_effects(contrasts * 2, variance, mask)
```

### Step 18: Call compute_fixed_effects()

```python
compute_fixed_effects(contrasts, variance, mask, dofs=[100])
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'Test the fixed effects performed manually/explicitly.'
shapes, rk = ([(*shape_3d_default, 4), (*shape_3d_default, 5)], 3)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk=rk)
contrast = np.eye(rk)[1]
multi_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[:1])
dic1 = multi_run_model.compute_contrast(contrast, output_type='all')
multi_run_model.fit(fmri_data[1], design_matrices=design_matrices[1:])
dic2 = multi_run_model.compute_contrast(contrast, output_type='all')
multi_run_model.fit(fmri_data, design_matrices=design_matrices)
fixed_fx_dic = multi_run_model.compute_contrast(contrast, output_type='all')
contrasts = [dic1['effect_size'], dic2['effect_size']]
variance = [dic1['effect_variance'], dic2['effect_variance']]
fixed_fx_contrast, fixed_fx_variance, fixed_fx_stat, _ = compute_fixed_effects(contrasts, variance, mask)
assert_almost_equal(get_data(fixed_fx_contrast), get_data(fixed_fx_dic['effect_size']))
assert_almost_equal(get_data(fixed_fx_variance), get_data(fixed_fx_dic['effect_variance']))
assert_almost_equal(get_data(fixed_fx_stat), get_data(fixed_fx_dic['stat']))
with pytest.raises(ValueError, match='The number of contrast images .* differs from the number of variance images'):
    compute_fixed_effects(contrasts * 2, variance, mask)
with pytest.raises(ValueError, match='degrees of freedom .* differs .* contrast images'):
    compute_fixed_effects(contrasts, variance, mask, dofs=[100])
```

## Next Steps


---

*Source: test_first_level.py:168 | Complexity: Advanced | Last updated: 2026-05-18*