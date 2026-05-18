# How To: Fmri Inputs Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test several errors with non_parametric_inference.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn._utils.data_gen`
- `nilearn.exceptions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.reporting`
- `conftest`

**Setup Required:**
```python
# Fixtures: rng, confounds, shape_3d_default, shape_4d_default
```

## Step-by-Step Guide

### Step 1: 'Test several errors with non_parametric_inference.'

```python
'Test several errors with non_parametric_inference.'
```

### Step 2: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design([shape_4d_default], rk=1)
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

### Step 6: Assign sdes = pd.DataFrame(...)

```python
sdes = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
```

### Step 7: Assign shape_3d = value

```python
shape_3d = [(*shape_3d_default, 1)]
```

### Step 8: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
_, fmri_data, _ = generate_fake_fmri_data_and_design(shape_3d)
```

### Step 9: Assign fmri_data = value

```python
fmri_data = fmri_data[0]
```

### Step 10: Assign niimgs = value

```python
niimgs = [fmri_data, fmri_data, fmri_data]
```

### Step 11: Assign niimg_4d = concat_imgs(...)

```python
niimg_4d = concat_imgs(niimgs)
```

### Step 12: Assign match = 'No second-level contrast is specified.'

```python
match = 'No second-level contrast is specified.'
```

### Step 13: Call non_parametric_inference()

```python
non_parametric_inference(niimgs, None, sdes)
```

### Step 14: Call non_parametric_inference()

```python
non_parametric_inference(niimgs, confounds, sdes)
```

### Step 15: Call non_parametric_inference()

```python
non_parametric_inference(niimg_4d, None, sdes)
```

### Step 16: Call non_parametric_inference()

```python
non_parametric_inference(flm)
```

### Step 17: Call non_parametric_inference()

```python
non_parametric_inference([fmri_data])
```

### Step 18: Call non_parametric_inference()

```python
non_parametric_inference(niimgs)
```

### Step 19: Call non_parametric_inference()

```python
non_parametric_inference([*niimgs, []], confounds)
```

### Step 20: Call non_parametric_inference()

```python
non_parametric_inference('random string object')
```


## Complete Example

```python
# Setup
# Fixtures: rng, confounds, shape_3d_default, shape_4d_default

# Workflow
'Test several errors with non_parametric_inference.'
_, fmri_data, design_matrices = generate_fake_fmri_data_and_design([shape_4d_default], rk=1)
flm = FirstLevelModel(subject_label='01').fit(fmri_data, design_matrices=design_matrices)
p, q = (80, 10)
X = rng.standard_normal(size=(p, q))
sdes = pd.DataFrame(X[:3, :3], columns=['intercept', 'b', 'c'])
shape_3d = [(*shape_3d_default, 1)]
_, fmri_data, _ = generate_fake_fmri_data_and_design(shape_3d)
fmri_data = fmri_data[0]
niimgs = [fmri_data, fmri_data, fmri_data]
niimg_4d = concat_imgs(niimgs)
match = 'No second-level contrast is specified.'
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimgs, None, sdes)
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimgs, confounds, sdes)
with pytest.raises(ValueError, match=match):
    non_parametric_inference(niimg_4d, None, sdes)
with pytest.raises(TypeError, match='second_level_input must be'):
    non_parametric_inference(flm)
with pytest.raises(TypeError, match='at least two'):
    non_parametric_inference([fmri_data])
with pytest.raises(ValueError, match='require a design matrix'):
    non_parametric_inference(niimgs)
with pytest.raises(TypeError):
    non_parametric_inference([*niimgs, []], confounds)
with pytest.raises(ValueError, match='File not found: .*'):
    non_parametric_inference('random string object')
```

## Next Steps


---

*Source: test_non_parametric_inference.py:125 | Complexity: Advanced | Last updated: 2026-05-18*