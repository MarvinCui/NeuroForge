# How To: Dki Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dki errors

## Prerequisites

**Required Modules:**
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dki`
- `dipy.reconst.dki`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.utils`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`


## Step-by-Step Guide

### Step 1: Call assert_raises()

```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='JOANA')
```

**Verification:**
```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='JOANA')
```

### Step 2: Call assert_raises()

```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, min_signal=-1)
```

**Verification:**
```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, min_signal=-1)
```

### Step 3: Assign dkiM = dki.DiffusionKurtosisModel(...)

```python
dkiM = dki.DiffusionKurtosisModel(gtab_2s, min_signal=1)
```

**Verification:**
```python
assert_array_almost_equal(dkiF.model_params, multi_params)
```

### Step 4: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

**Verification:**
```python
assert_array_almost_equal(dkiF.model_params, multi_params)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dkiF.model_params, multi_params)
```

**Verification:**
```python
assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
```

### Step 6: Assign dkiM = dki.DiffusionKurtosisModel(...)

```python
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
```

**Verification:**
```python
assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
```

### Step 7: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

**Verification:**
```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab)
```

### Step 8: Assign mask_correct = value

```python
mask_correct = dkiF.fa > 0
```

**Verification:**
```python
assert_raises(TripWireError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='NLS')
```

### Step 9: Assign unknown = False

```python
mask_correct[1, 1] = False
```

**Verification:**
```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level='all')
```

### Step 10: Assign unknown = np.zeros(...)

```python
multi_params[1, 1] = np.zeros(27)
```

**Verification:**
```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level=3)
```

### Step 11: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI, mask=mask_correct)
```

**Verification:**
```python
assert_almost_equal(dkim.convexity_level, 4)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(dkiF.model_params, multi_params)
```

### Step 13: Assign mask_not_correct = np.array(...)

```python
mask_not_correct = np.array([[True, True, False], [True, False, False]])
```

### Step 14: Call assert_raises()

```python
assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
```

### Step 15: Assign dkiM = dki.DiffusionKurtosisModel(...)

```python
dkiM = dki.DiffusionKurtosisModel(gtab_2s, fit_method='NLS')
```

### Step 16: Call assert_raises()

```python
assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
```

### Step 17: Call assert_raises()

```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab)
```

### Step 18: Call assert_raises()

```python
assert_raises(TripWireError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='NLS')
```

### Step 19: Call assert_raises()

```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level='all')
```

### Step 20: Call assert_raises()

```python
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level=3)
```

### Step 21: Assign dkim = dki.DiffusionKurtosisModel(...)

```python
dkim = dki.DiffusionKurtosisModel(gtab_2s, fit_method='CLS', convexity_level=6)
```

### Step 22: Call check_for_warnings()

```python
check_for_warnings(l_warns, 'Maximum convexity_level supported is 4.')
```

### Step 23: Call assert_almost_equal()

```python
assert_almost_equal(dkim.convexity_level, 4)
```


## Complete Example

```python
# Workflow
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='JOANA')
assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, min_signal=-1)
dkiM = dki.DiffusionKurtosisModel(gtab_2s, min_signal=1)
dkiF = dkiM.fit(DWI)
assert_array_almost_equal(dkiF.model_params, multi_params)
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
dkiF = dkiM.fit(DWI)
mask_correct = dkiF.fa > 0
mask_correct[1, 1] = False
multi_params[1, 1] = np.zeros(27)
dkiF = dkiM.fit(DWI, mask=mask_correct)
assert_array_almost_equal(dkiF.model_params, multi_params)
mask_not_correct = np.array([[True, True, False], [True, False, False]])
assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
if have_cvxpy:
    dkiM = dki.DiffusionKurtosisModel(gtab_2s, fit_method='NLS')
    assert_raises(ValueError, dkiM.fit, DWI, mask=mask_not_correct)
    assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab)
else:
    assert_raises(TripWireError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='NLS')
if have_cvxpy:
    assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level='all')
    assert_raises(ValueError, dki.DiffusionKurtosisModel, gtab_2s, fit_method='CLS', convexity_level=3)
    with warnings.catch_warnings(record=True) as l_warns:
        dkim = dki.DiffusionKurtosisModel(gtab_2s, fit_method='CLS', convexity_level=6)
        check_for_warnings(l_warns, 'Maximum convexity_level supported is 4.')
        assert_almost_equal(dkim.convexity_level, 4)
```

## Next Steps


---

*Source: test_dki.py:887 | Complexity: Advanced | Last updated: 2026-05-18*