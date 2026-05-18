# How To: Default Lambda Csdmodel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: We check that the default value of lambda is the expected value with
the symmetric362 sphere. This value has empirically been found to work well
and changes to this default value should be discussed with the dipy team.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.gradients`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: 'We check that the default value of lambda is the expected value with\n    the symmetric362 sphere. This value has empirically been found to work well\n    and changes to this default value should be discussed with the dipy team.\n    '

```python
'We check that the default value of lambda is the expected value with\n    the symmetric362 sphere. This value has empirically been found to work well\n    and changes to this default value should be discussed with the dipy team.\n    '
```

### Step 2: Assign expected_lambda = value

```python
expected_lambda = {4: 27.5230088, 8: 82.5713865, 16: 216.0843135}
```

### Step 3: Assign expected_csdmodel_warnings = value

```python
expected_csdmodel_warnings = {4: 0, 8: 0, 16: 1}
```

### Step 4: Assign expected_sh_basis_deprecation_warnings = 3

```python
expected_sh_basis_deprecation_warnings = 3
```

### Step 5: Assign sphere = default_sphere

```python
sphere = default_sphere
```

### Step 6: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

### Step 7: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 8: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 9: Assign response = value

```python
response = (np.array([0.0015, 0.0003, 0.0003]), 100)
```

### Step 10: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(model_full.B_reg, expected * B_reg)
```

### Step 11: Call warnings.simplefilter()

```python
warnings.simplefilter('always', category=PendingDeprecationWarning)
```

### Step 12: Assign s_o_m = sh_order_max

```python
s_o_m = sh_order_max
```

### Step 13: Assign model_full = ConstrainedSphericalDeconvModel(...)

```python
model_full = ConstrainedSphericalDeconvModel(gtab, response, sh_order_max=s_o_m, reg_sphere=sphere)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(len(w) - expected_sh_basis_deprecation_warnings, e_warn)
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign unknown = real_sh_descoteaux(...)

```python
B_reg, _, _ = real_sh_descoteaux(sh_order_max, sphere.theta, sphere.phi)
```

### Step 17: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, UserWarning))
```

### Step 18: Call npt.assert_()

```python
npt.assert_('Number of parameters required ' in str(w[0].message))
```


## Complete Example

```python
# Workflow
'We check that the default value of lambda is the expected value with\n    the symmetric362 sphere. This value has empirically been found to work well\n    and changes to this default value should be discussed with the dipy team.\n    '
expected_lambda = {4: 27.5230088, 8: 82.5713865, 16: 216.0843135}
expected_csdmodel_warnings = {4: 0, 8: 0, 16: 1}
expected_sh_basis_deprecation_warnings = 3
sphere = default_sphere
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
response = (np.array([0.0015, 0.0003, 0.0003]), 100)
for sh_order_max, expected, e_warn in zip(expected_lambda.keys(), expected_lambda.values(), expected_csdmodel_warnings.values()):
    with warnings.catch_warnings(record=True) as w:
        warnings.simplefilter('always', category=PendingDeprecationWarning)
        s_o_m = sh_order_max
        model_full = ConstrainedSphericalDeconvModel(gtab, response, sh_order_max=s_o_m, reg_sphere=sphere)
        npt.assert_equal(len(w) - expected_sh_basis_deprecation_warnings, e_warn)
        if e_warn:
            npt.assert_(issubclass(w[0].category, UserWarning))
            npt.assert_('Number of parameters required ' in str(w[0].message))
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
        B_reg, _, _ = real_sh_descoteaux(sh_order_max, sphere.theta, sphere.phi)
    npt.assert_array_almost_equal(model_full.B_reg, expected * B_reg)
```

## Next Steps


---

*Source: test_csdeconv.py:720 | Complexity: Advanced | Last updated: 2026-05-18*