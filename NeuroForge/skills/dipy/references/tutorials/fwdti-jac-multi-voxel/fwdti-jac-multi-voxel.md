# How To: Fwdti Jac Multi Voxel

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti jac multi voxel

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.fwdti`
- `dipy.reconst.fwdti`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS')
```

**Verification:**
```python
assert_array_almost_equal(Ffwe, GTF[0, :])
```

### Step 2: Call fwdm.fit()

```python
fwdm.fit(DWI[0, :, :])
```

**Verification:**
```python
assert_array_almost_equal(Ffwe, GTF[0, :])
```

### Step 3: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', f_transform=False, jac=True)
```

### Step 4: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI[0, :, :])
```

### Step 5: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Ffwe, GTF[0, :])
```

### Step 7: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', f_transform=True, jac=True)
```

### Step 8: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI[0, :, :])
```

### Step 9: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(Ffwe, GTF[0, :])
```


## Complete Example

```python
# Workflow
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS')
fwdm.fit(DWI[0, :, :])
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', f_transform=False, jac=True)
fwefit = fwdm.fit(DWI[0, :, :])
Ffwe = fwefit.f
assert_array_almost_equal(Ffwe, GTF[0, :])
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', f_transform=True, jac=True)
fwefit = fwdm.fit(DWI[0, :, :])
Ffwe = fwefit.f
assert_array_almost_equal(Ffwe, GTF[0, :])
```

## Next Steps


---

*Source: test_fwdti.py:276 | Complexity: Advanced | Last updated: 2026-05-18*