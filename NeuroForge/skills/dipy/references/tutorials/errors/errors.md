# How To: Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test errors

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.msdki`
- `dipy.reconst.msdki`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Call assert_raises()

```python
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab)
```

**Verification:**
```python
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab)
```

### Step 2: Call assert_raises()

```python
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab_3s, min_signal=-1)
```

**Verification:**
```python
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab_3s, min_signal=-1)
```

### Step 3: Assign mask_wrong = np.ones(...)

```python
mask_wrong = np.ones((2, 3, 1))
```

**Verification:**
```python
assert_raises(ValueError, msdki_model.fit, DWI, mask=mask_wrong)
```

### Step 4: Assign msdki_model = msdki.MeanDiffusionKurtosisModel(...)

```python
msdki_model = msdki.MeanDiffusionKurtosisModel(gtab_3s)
```

**Verification:**
```python
assert_raises(IndexError, aux_test_fun, mdkiF, (0, 0, 0, 0))
```

### Step 5: Call assert_raises()

```python
assert_raises(ValueError, msdki_model.fit, DWI, mask=mask_wrong)
```

**Verification:**
```python
assert_array_almost_equal(MKgt_multi[0, 0, 0], met)
```

### Step 6: Assign mdkiF = msdki_model.fit(...)

```python
mdkiF = msdki_model.fit(DWI)
```

**Verification:**
```python
assert_raises(ValueError, awf_from_msk, MKgt_multi, mask=mask_wrong)
```

### Step 7: Call assert_raises()

```python
assert_raises(IndexError, aux_test_fun, mdkiF, (0, 0, 0, 0))
```

### Step 8: Assign met = aux_test_fun(...)

```python
met = aux_test_fun(mdkiF, (0, 0, 0))
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(MKgt_multi[0, 0, 0], met)
```

### Step 10: Call assert_raises()

```python
assert_raises(ValueError, awf_from_msk, MKgt_multi, mask=mask_wrong)
```

### Step 11: Assign met = value

```python
met = ob[ind].msk
```


## Complete Example

```python
# Workflow
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab)
assert_raises(ValueError, msdki.MeanDiffusionKurtosisModel, gtab_3s, min_signal=-1)
mask_wrong = np.ones((2, 3, 1))
msdki_model = msdki.MeanDiffusionKurtosisModel(gtab_3s)
assert_raises(ValueError, msdki_model.fit, DWI, mask=mask_wrong)

def aux_test_fun(ob, ind):
    met = ob[ind].msk
    return met
mdkiF = msdki_model.fit(DWI)
assert_raises(IndexError, aux_test_fun, mdkiF, (0, 0, 0, 0))
met = aux_test_fun(mdkiF, (0, 0, 0))
assert_array_almost_equal(MKgt_multi[0, 0, 0], met)
assert_raises(ValueError, awf_from_msk, MKgt_multi, mask=mask_wrong)
```

## Next Steps


---

*Source: test_msdki.py:136 | Complexity: Advanced | Last updated: 2026-05-18*