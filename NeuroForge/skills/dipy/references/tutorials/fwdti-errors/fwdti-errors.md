# How To: Fwdti Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti errors

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

### Step 1: Call assert_raises()

```python
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab_2s, fit_method='pKT')
```

**Verification:**
```python
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab_2s, fit_method='pKT')
```

### Step 2: Assign fwdtiM = fwdti.FreeWaterTensorModel(...)

```python
fwdtiM = fwdti.FreeWaterTensorModel(gtab_2s)
```

**Verification:**
```python
assert_raises(ValueError, fwdtiM.fit, DWI, mask=incorrect_mask)
```

### Step 3: Assign incorrect_mask = np.array(...)

```python
incorrect_mask = np.array([[True, True, False], [True, False, False]])
```

**Verification:**
```python
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab)
```

### Step 4: Call assert_raises()

```python
assert_raises(ValueError, fwdtiM.fit, DWI, mask=incorrect_mask)
```

**Verification:**
```python
assert_array_almost_equal(fwdtiF.fa, FAref)
```

### Step 5: Call assert_raises()

```python
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab)
```

**Verification:**
```python
assert_array_almost_equal(fwdtiF.f, GTF)
```

### Step 6: Assign fwdtiM = fwdti.FreeWaterTensorModel(...)

```python
fwdtiM = fwdti.FreeWaterTensorModel(gtab_2s, min_signal=1)
```

**Verification:**
```python
assert_raises(ValueError, fwdm.fit, DWI)
```

### Step 7: Assign correct_mask = np.zeros(...)

```python
correct_mask = np.zeros((2, 2, 2))
```

### Step 8: Assign unknown = 1

```python
correct_mask[0, :, :] = 1
```

### Step 9: Assign correct_mask = value

```python
correct_mask = correct_mask > 0
```

### Step 10: Assign fwdtiF = fwdtiM.fit(...)

```python
fwdtiF = fwdtiM.fit(DWI, mask=correct_mask)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF.fa, FAref)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF.f, GTF)
```

### Step 13: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='sigma')
```

### Step 14: Call assert_raises()

```python
assert_raises(ValueError, fwdm.fit, DWI)
```


## Complete Example

```python
# Workflow
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab_2s, fit_method='pKT')
fwdtiM = fwdti.FreeWaterTensorModel(gtab_2s)
incorrect_mask = np.array([[True, True, False], [True, False, False]])
assert_raises(ValueError, fwdtiM.fit, DWI, mask=incorrect_mask)
assert_raises(ValueError, fwdti.FreeWaterTensorModel, gtab)
fwdtiM = fwdti.FreeWaterTensorModel(gtab_2s, min_signal=1)
correct_mask = np.zeros((2, 2, 2))
correct_mask[0, :, :] = 1
correct_mask = correct_mask > 0
fwdtiF = fwdtiM.fit(DWI, mask=correct_mask)
assert_array_almost_equal(fwdtiF.fa, FAref)
assert_array_almost_equal(fwdtiF.f, GTF)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='sigma')
assert_raises(ValueError, fwdm.fit, DWI)
```

## Next Steps


---

*Source: test_fwdti.py:217 | Complexity: Advanced | Last updated: 2026-05-18*