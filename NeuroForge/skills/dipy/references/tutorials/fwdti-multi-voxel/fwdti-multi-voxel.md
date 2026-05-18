# How To: Fwdti Multi Voxel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti multi voxel

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
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=False)
```

**Verification:**
```python
assert_almost_equal(FAfwe, FAref)
```

### Step 2: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI)
```

**Verification:**
```python
assert_almost_equal(Ffwe, GTF)
```

### Step 3: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

**Verification:**
```python
assert_almost_equal(MDfwe, MDref)
```

### Step 4: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

**Verification:**
```python
assert_almost_equal(FAfwe, FAref)
```

### Step 5: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

**Verification:**
```python
assert_almost_equal(Ffwe, GTF)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(FAfwe, FAref)
```

**Verification:**
```python
assert_almost_equal(MDfwe, MDref)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, GTF)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDref)
```

### Step 9: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=True)
```

### Step 10: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI)
```

### Step 11: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

### Step 12: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 13: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(FAfwe, FAref)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, GTF)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDref)
```


## Complete Example

```python
# Workflow
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=False)
fwefit = fwdm.fit(DWI)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAfwe, FAref)
assert_almost_equal(Ffwe, GTF)
assert_almost_equal(MDfwe, MDref)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=True)
fwefit = fwdm.fit(DWI)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAfwe, FAref)
assert_almost_equal(Ffwe, GTF)
assert_almost_equal(MDfwe, MDref)
```

## Next Steps


---

*Source: test_fwdti.py:155 | Complexity: Advanced | Last updated: 2026-05-18*