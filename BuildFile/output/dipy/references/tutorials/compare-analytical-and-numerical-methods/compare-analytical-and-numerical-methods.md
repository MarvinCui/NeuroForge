# How To: Compare Analytical And Numerical Methods

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compare analytical and numerical methods

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

### Step 1: Assign dkiM = dki.DiffusionKurtosisModel(...)

```python
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
```

**Verification:**
```python
assert_array_almost_equal(MK_as, MK_nm)
```

### Step 2: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(signal_cross)
```

**Verification:**
```python
assert_array_almost_equal(RK_as, RK_nm)
```

### Step 3: Assign MK_as = dkiF.rk(...)

```python
MK_as = dkiF.rk(analytical=True)
```

**Verification:**
```python
assert_array_almost_equal(AK_as, AK_nm)
```

### Step 4: Assign MK_nm = dkiF.rk(...)

```python
MK_nm = dkiF.rk(analytical=False)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(MK_as, MK_nm)
```

### Step 6: Assign RK_as = dkiF.rk(...)

```python
RK_as = dkiF.rk(analytical=True)
```

### Step 7: Assign RK_nm = dkiF.rk(...)

```python
RK_nm = dkiF.rk(analytical=False)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RK_as, RK_nm)
```

### Step 9: Assign AK_as = dkiF.ak(...)

```python
AK_as = dkiF.ak(analytical=True)
```

### Step 10: Assign AK_nm = dkiF.ak(...)

```python
AK_nm = dkiF.ak(analytical=False)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(AK_as, AK_nm)
```


## Complete Example

```python
# Workflow
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
dkiF = dkiM.fit(signal_cross)
MK_as = dkiF.rk(analytical=True)
MK_nm = dkiF.rk(analytical=False)
assert_array_almost_equal(MK_as, MK_nm)
RK_as = dkiF.rk(analytical=True)
RK_nm = dkiF.rk(analytical=False)
assert_array_almost_equal(RK_as, RK_nm)
AK_as = dkiF.ak(analytical=True)
AK_nm = dkiF.ak(analytical=False)
assert_array_almost_equal(AK_as, AK_nm)
```

## Next Steps


---

*Source: test_dki.py:813 | Complexity: Advanced | Last updated: 2026-05-18*