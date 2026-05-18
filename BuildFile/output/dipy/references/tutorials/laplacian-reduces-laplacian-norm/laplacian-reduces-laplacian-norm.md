# How To: Laplacian Reduces Laplacian Norm

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test laplacian reduces laplacian norm

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
assert_(laplacian_norm_no_reg > laplacian_norm_reg)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

### Step 3: Assign S = generate_signal_crossing(...)

```python
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
```

### Step 4: Assign qtdmri_mod_no_laplacian = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_no_laplacian = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, laplacian_regularization=True, laplacian_weighting=0.0)
```

### Step 5: Assign qtdmri_mod_laplacian = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_laplacian = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, laplacian_regularization=True, laplacian_weighting=0.0001)
```

### Step 6: Assign qtdmri_fit_no_laplacian = qtdmri_mod_no_laplacian.fit(...)

```python
qtdmri_fit_no_laplacian = qtdmri_mod_no_laplacian.fit(S)
```

### Step 7: Assign qtdmri_fit_laplacian = qtdmri_mod_laplacian.fit(...)

```python
qtdmri_fit_laplacian = qtdmri_mod_laplacian.fit(S)
```

### Step 8: Assign laplacian_norm_no_reg = qtdmri_fit_no_laplacian.norm_of_laplacian_signal(...)

```python
laplacian_norm_no_reg = qtdmri_fit_no_laplacian.norm_of_laplacian_signal()
```

### Step 9: Assign laplacian_norm_reg = qtdmri_fit_laplacian.norm_of_laplacian_signal(...)

```python
laplacian_norm_reg = qtdmri_fit_laplacian.norm_of_laplacian_signal()
```

### Step 10: Call assert_()

```python
assert_(laplacian_norm_no_reg > laplacian_norm_reg)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order

# Workflow
gtab_4d = generate_gtab4D()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
qtdmri_mod_no_laplacian = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, laplacian_regularization=True, laplacian_weighting=0.0)
qtdmri_mod_laplacian = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, laplacian_regularization=True, laplacian_weighting=0.0001)
qtdmri_fit_no_laplacian = qtdmri_mod_no_laplacian.fit(S)
qtdmri_fit_laplacian = qtdmri_mod_laplacian.fit(S)
laplacian_norm_no_reg = qtdmri_fit_no_laplacian.norm_of_laplacian_signal()
laplacian_norm_reg = qtdmri_fit_laplacian.norm_of_laplacian_signal()
assert_(laplacian_norm_no_reg > laplacian_norm_reg)
```

## Next Steps


---

*Source: test_qtdmri.py:563 | Complexity: Advanced | Last updated: 2026-05-18*