# How To: Cartesian Normalization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cartesian normalization

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.integrate`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: radial_order, time_order
```

## Step-by-Step Guide

### Step 1: Assign gtab_4d = generate_gtab4D(...)

```python
gtab_4d = generate_gtab4D()
```

**Verification:**
```python
assert_array_almost_equal(qtdmri_fit_aniso.fitted_signal(), qtdmri_fit_aniso_norm.fitted_signal())
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

**Verification:**
```python
assert_array_almost_equal(pdf_aniso / pdf_aniso.max(), pdf_aniso_norm / pdf_aniso.max())
```

### Step 3: Assign S = generate_signal_crossing(...)

```python
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
```

**Verification:**
```python
assert_array_almost_equal(norm_laplacian / norm_laplacian, norm_laplacian_norm / norm_laplacian)
```

### Step 4: Assign qtdmri_mod_aniso = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, normalization=False)
```

### Step 5: Assign qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, normalization=True)
```

### Step 6: Assign qtdmri_fit_aniso = qtdmri_mod_aniso.fit(...)

```python
qtdmri_fit_aniso = qtdmri_mod_aniso.fit(S)
```

### Step 7: Assign qtdmri_fit_aniso_norm = qtdmri_mod_aniso_norm.fit(...)

```python
qtdmri_fit_aniso_norm = qtdmri_mod_aniso_norm.fit(S)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(qtdmri_fit_aniso.fitted_signal(), qtdmri_fit_aniso_norm.fitted_signal())
```

### Step 9: Assign rt_grid = qtdmri.create_rt_space_grid(...)

```python
rt_grid = qtdmri.create_rt_space_grid(5, 0.02, 5, 0.02, 0.05)
```

### Step 10: Assign pdf_aniso = qtdmri_fit_aniso.pdf(...)

```python
pdf_aniso = qtdmri_fit_aniso.pdf(rt_grid)
```

### Step 11: Assign pdf_aniso_norm = qtdmri_fit_aniso_norm.pdf(...)

```python
pdf_aniso_norm = qtdmri_fit_aniso_norm.pdf(rt_grid)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pdf_aniso / pdf_aniso.max(), pdf_aniso_norm / pdf_aniso.max())
```

### Step 13: Assign norm_laplacian = qtdmri_fit_aniso.norm_of_laplacian_signal(...)

```python
norm_laplacian = qtdmri_fit_aniso.norm_of_laplacian_signal()
```

### Step 14: Assign norm_laplacian_norm = qtdmri_fit_aniso_norm.norm_of_laplacian_signal(...)

```python
norm_laplacian_norm = qtdmri_fit_aniso_norm.norm_of_laplacian_signal()
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(norm_laplacian / norm_laplacian, norm_laplacian_norm / norm_laplacian)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order

# Workflow
gtab_4d = generate_gtab4D()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, normalization=False)
qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, normalization=True)
qtdmri_fit_aniso = qtdmri_mod_aniso.fit(S)
qtdmri_fit_aniso_norm = qtdmri_mod_aniso_norm.fit(S)
assert_array_almost_equal(qtdmri_fit_aniso.fitted_signal(), qtdmri_fit_aniso_norm.fitted_signal())
rt_grid = qtdmri.create_rt_space_grid(5, 0.02, 5, 0.02, 0.05)
pdf_aniso = qtdmri_fit_aniso.pdf(rt_grid)
pdf_aniso_norm = qtdmri_fit_aniso_norm.pdf(rt_grid)
assert_array_almost_equal(pdf_aniso / pdf_aniso.max(), pdf_aniso_norm / pdf_aniso.max())
norm_laplacian = qtdmri_fit_aniso.norm_of_laplacian_signal()
norm_laplacian_norm = qtdmri_fit_aniso_norm.norm_of_laplacian_signal()
assert_array_almost_equal(norm_laplacian / norm_laplacian, norm_laplacian_norm / norm_laplacian)
```

## Next Steps


---

*Source: test_qtdmri.py:306 | Complexity: Advanced | Last updated: 2026-05-18*