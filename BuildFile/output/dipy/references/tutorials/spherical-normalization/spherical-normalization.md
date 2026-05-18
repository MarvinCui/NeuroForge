# How To: Spherical Normalization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test spherical normalization

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
assert_array_almost_equal(qtdmri_fit.fitted_signal(), qtdmri_fit_norm.fitted_signal())
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

**Verification:**
```python
assert_array_almost_equal(pdf / pdf.max(), pdf_norm / pdf.max())
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
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=False, normalization=False)
```

### Step 5: Assign qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=False, normalization=True)
```

### Step 6: Assign rt_grid = qtdmri.create_rt_space_grid(...)

```python
rt_grid = qtdmri.create_rt_space_grid(5, 0.02, 5, 0.02, 0.05)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pdf / pdf.max(), pdf_norm / pdf.max())
```

### Step 8: Assign norm_laplacian = qtdmri_fit.norm_of_laplacian_signal(...)

```python
norm_laplacian = qtdmri_fit.norm_of_laplacian_signal()
```

### Step 9: Assign norm_laplacian_norm = qtdmri_fit_norm.norm_of_laplacian_signal(...)

```python
norm_laplacian_norm = qtdmri_fit_norm.norm_of_laplacian_signal()
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(norm_laplacian / norm_laplacian, norm_laplacian_norm / norm_laplacian)
```

### Step 11: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 12: Assign qtdmri_fit = qtdmri_mod_aniso.fit(...)

```python
qtdmri_fit = qtdmri_mod_aniso.fit(S)
```

### Step 13: Assign qtdmri_fit_norm = qtdmri_mod_aniso_norm.fit(...)

```python
qtdmri_fit_norm = qtdmri_mod_aniso_norm.fit(S)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(qtdmri_fit.fitted_signal(), qtdmri_fit_norm.fitted_signal())
```

### Step 15: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 16: Assign pdf = qtdmri_fit.pdf(...)

```python
pdf = qtdmri_fit.pdf(rt_grid)
```

### Step 17: Assign pdf_norm = qtdmri_fit_norm.pdf(...)

```python
pdf_norm = qtdmri_fit_norm.pdf(rt_grid)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order

# Workflow
gtab_4d = generate_gtab4D()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=False, normalization=False)
qtdmri_mod_aniso_norm = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=False, normalization=True)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    qtdmri_fit = qtdmri_mod_aniso.fit(S)
    qtdmri_fit_norm = qtdmri_mod_aniso_norm.fit(S)
    assert_array_almost_equal(qtdmri_fit.fitted_signal(), qtdmri_fit_norm.fitted_signal())
rt_grid = qtdmri.create_rt_space_grid(5, 0.02, 5, 0.02, 0.05)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    pdf = qtdmri_fit.pdf(rt_grid)
    pdf_norm = qtdmri_fit_norm.pdf(rt_grid)
assert_array_almost_equal(pdf / pdf.max(), pdf_norm / pdf.max())
norm_laplacian = qtdmri_fit.norm_of_laplacian_signal()
norm_laplacian_norm = qtdmri_fit_norm.norm_of_laplacian_signal()
assert_array_almost_equal(norm_laplacian / norm_laplacian, norm_laplacian_norm / norm_laplacian)
```

## Next Steps


---

*Source: test_qtdmri.py:343 | Complexity: Advanced | Last updated: 2026-05-18*