# How To: Anisotropic Reduced Mse

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test anisotropic reduced MSE

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
assert_(mse_aniso < mse_iso)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

### Step 3: Assign S = generate_signal_crossing(...)

```python
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
```

### Step 4: Assign qtdmri_mod_aniso = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, anisotropic_scaling=True)
```

### Step 5: Assign qtdmri_mod_iso = qtdmri.QtdmriModel(...)

```python
qtdmri_mod_iso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, anisotropic_scaling=False)
```

### Step 6: Assign qtdmri_fit_aniso = qtdmri_mod_aniso.fit(...)

```python
qtdmri_fit_aniso = qtdmri_mod_aniso.fit(S)
```

### Step 7: Assign qtdmri_fit_iso = qtdmri_mod_iso.fit(...)

```python
qtdmri_fit_iso = qtdmri_mod_iso.fit(S)
```

### Step 8: Assign mse_aniso = np.mean(...)

```python
mse_aniso = np.mean((S - qtdmri_fit_aniso.fitted_signal()) ** 2)
```

### Step 9: Assign mse_iso = np.mean(...)

```python
mse_iso = np.mean((S - qtdmri_fit_iso.fitted_signal()) ** 2)
```

### Step 10: Call assert_()

```python
assert_(mse_aniso < mse_iso)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order

# Workflow
gtab_4d = generate_gtab4D()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
qtdmri_mod_aniso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, anisotropic_scaling=True)
qtdmri_mod_iso = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order, cartesian=True, anisotropic_scaling=False)
qtdmri_fit_aniso = qtdmri_mod_aniso.fit(S)
qtdmri_fit_iso = qtdmri_mod_iso.fit(S)
mse_aniso = np.mean((S - qtdmri_fit_aniso.fitted_signal()) ** 2)
mse_iso = np.mean((S - qtdmri_fit_iso.fitted_signal()) ** 2)
assert_(mse_aniso < mse_iso)
```

## Next Steps


---

*Source: test_qtdmri.py:392 | Complexity: Advanced | Last updated: 2026-05-18*