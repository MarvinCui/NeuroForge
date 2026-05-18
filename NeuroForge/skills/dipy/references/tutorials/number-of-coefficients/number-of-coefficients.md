# How To: Number Of Coefficients

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test number of coefficients

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
assert_equal(number_of_coef_model, number_of_coef_analytic)
```

### Step 2: Assign unknown = value

```python
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
```

### Step 3: Assign S = generate_signal_crossing(...)

```python
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
```

### Step 4: Assign qtdmri_mod = qtdmri.QtdmriModel(...)

```python
qtdmri_mod = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order)
```

### Step 5: Assign qtdmri_fit = qtdmri_mod.fit(...)

```python
qtdmri_fit = qtdmri_mod.fit(S)
```

### Step 6: Assign number_of_coef_model = value

```python
number_of_coef_model = qtdmri_fit._qtdmri_coef.shape[0]
```

### Step 7: Assign number_of_coef_analytic = qtdmri.qtdmri_number_of_coefficients(...)

```python
number_of_coef_analytic = qtdmri.qtdmri_number_of_coefficients(radial_order, time_order)
```

### Step 8: Call assert_equal()

```python
assert_equal(number_of_coef_model, number_of_coef_analytic)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order

# Workflow
gtab_4d = generate_gtab4D()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S = generate_signal_crossing(gtab_4d, l1, l2, l3)
qtdmri_mod = qtdmri.QtdmriModel(gtab_4d, radial_order=radial_order, time_order=time_order)
qtdmri_fit = qtdmri_mod.fit(S)
number_of_coef_model = qtdmri_fit._qtdmri_coef.shape[0]
number_of_coef_analytic = qtdmri.qtdmri_number_of_coefficients(radial_order, time_order)
assert_equal(number_of_coef_model, number_of_coef_analytic)
```

## Next Steps


---

*Source: test_qtdmri.py:417 | Complexity: Advanced | Last updated: 2026-05-18*