# How To: Sh To Bingham Handles Empty Voxels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Regression test for UnboundLocalError in sh_to_bingham (Issue #3638).

Uses  small DWI dataset to fit SH coefficients via CSA ODF,
then verifies that sh_to_bingham handles empty voxels correctly.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.bingham`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: 'Regression test for UnboundLocalError in sh_to_bingham (Issue #3638).\n\n    Uses  small DWI dataset to fit SH coefficients via CSA ODF,\n    then verifies that sh_to_bingham handles empty voxels correctly.\n    '

```python
'Regression test for UnboundLocalError in sh_to_bingham (Issue #3638).\n\n    Uses  small DWI dataset to fit SH coefficients via CSA ODF,\n    then verifies that sh_to_bingham handles empty voxels correctly.\n    '
```

**Verification:**
```python
assert bim.model_params.shape[:3] == sh_coeff.shape[:3]
```

### Step 2: Assign unknown = get_fnames(...)

```python
dwi_fname, bval_fname, bvec_fname = get_fnames(name='small_64D')
```

### Step 3: Assign data = load_nifti_data(...)

```python
data = load_nifti_data(dwi_fname)
```

### Step 4: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(bval_fname, bvec_fname)
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals=bvals, bvecs=bvecs)
```

### Step 6: Assign sh_coeff = sh_coeff.copy(...)

```python
sh_coeff = sh_coeff.copy()
```

### Step 7: Assign unknown = 0

```python
sh_coeff[0, 0, 0, :] = 0
```

### Step 8: Assign sphere = get_sphere.subdivide(...)

```python
sphere = get_sphere(name='repulsion724').subdivide(n=2)
```

### Step 9: Assign bim = sh_to_bingham(...)

```python
bim = sh_to_bingham(sh_coeff, sphere, legacy=False, max_search_angle=45)
```

**Verification:**
```python
assert bim.model_params.shape[:3] == sh_coeff.shape[:3]
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign csa_model = CsaOdfModel(...)

```python
csa_model = CsaOdfModel(gtab, sh_order_max=4)
```

### Step 12: Assign csa_fit = csa_model.fit(...)

```python
csa_fit = csa_model.fit(data)
```

### Step 13: Assign sh_coeff = value

```python
sh_coeff = csa_fit.shm_coeff
```


## Complete Example

```python
# Workflow
'Regression test for UnboundLocalError in sh_to_bingham (Issue #3638).\n\n    Uses  small DWI dataset to fit SH coefficients via CSA ODF,\n    then verifies that sh_to_bingham handles empty voxels correctly.\n    '
dwi_fname, bval_fname, bvec_fname = get_fnames(name='small_64D')
data = load_nifti_data(dwi_fname)
bvals, bvecs = read_bvals_bvecs(bval_fname, bvec_fname)
gtab = gradient_table(bvals=bvals, bvecs=bvecs)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    csa_model = CsaOdfModel(gtab, sh_order_max=4)
    csa_fit = csa_model.fit(data)
    sh_coeff = csa_fit.shm_coeff
sh_coeff = sh_coeff.copy()
sh_coeff[0, 0, 0, :] = 0
sphere = get_sphere(name='repulsion724').subdivide(n=2)
bim = sh_to_bingham(sh_coeff, sphere, legacy=False, max_search_angle=45)
assert bim.model_params.shape[:3] == sh_coeff.shape[:3]
```

## Next Steps


---

*Source: test_bingham.py:231 | Complexity: Advanced | Last updated: 2026-05-18*