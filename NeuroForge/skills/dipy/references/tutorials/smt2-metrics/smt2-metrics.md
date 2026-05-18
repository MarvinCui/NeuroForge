# How To: Smt2 Metrics

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test smt2 metrics

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

### Step 1: Assign AWFgt = awf_from_msk(...)

```python
AWFgt = awf_from_msk(MKgt_multi)
```

**Verification:**
```python
assert_array_almost_equal(mdkiF.smt2f, AWFgt)
```

### Step 2: Assign DIgt = value

```python
DIgt = 3 * MDgt_multi / (1 + 2 * (1 - AWFgt) ** 2)
```

**Verification:**
```python
assert_array_almost_equal(mdkiF.smt2di, DIgt)
```

### Step 3: Assign RDe = value

```python
RDe = DIgt * (1 - AWFgt)
```

**Verification:**
```python
assert_array_almost_equal(mdkiF.smt2uFA[MD > 0], uFAgt)
```

### Step 4: Assign VarD = value

```python
VarD = 2 / 9 * (AWFgt * DIgt ** 2 + (1 - AWFgt) * (DIgt - RDe) ** 2)
```

**Verification:**
```python
assert_array_almost_equal(AWF, AWFgt)
```

### Step 5: Assign MD = value

```python
MD = (AWFgt * DIgt + (1 - AWFgt) * (DIgt + 2 * RDe)) / 3
```

### Step 6: Assign uFAgt = np.sqrt(...)

```python
uFAgt = np.sqrt(3 / 2 * VarD[MD > 0] / (VarD[MD > 0] + MD[MD > 0] ** 2))
```

### Step 7: Assign mdkiM = msdki.MeanDiffusionKurtosisModel(...)

```python
mdkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
```

### Step 8: Assign mdkiF = mdkiM.fit(...)

```python
mdkiF = mdkiM.fit(DWI)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(mdkiF.smt2f, AWFgt)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(mdkiF.smt2di, DIgt)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(mdkiF.smt2uFA[MD > 0], uFAgt)
```

### Step 12: Assign mask = value

```python
mask = MKgt_multi > 0
```

### Step 13: Assign AWF = awf_from_msk(...)

```python
AWF = awf_from_msk(MKgt_multi, mask=mask)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(AWF, AWFgt)
```


## Complete Example

```python
# Workflow
AWFgt = awf_from_msk(MKgt_multi)
DIgt = 3 * MDgt_multi / (1 + 2 * (1 - AWFgt) ** 2)
RDe = DIgt * (1 - AWFgt)
VarD = 2 / 9 * (AWFgt * DIgt ** 2 + (1 - AWFgt) * (DIgt - RDe) ** 2)
MD = (AWFgt * DIgt + (1 - AWFgt) * (DIgt + 2 * RDe)) / 3
uFAgt = np.sqrt(3 / 2 * VarD[MD > 0] / (VarD[MD > 0] + MD[MD > 0] ** 2))
mdkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
mdkiF = mdkiM.fit(DWI)
assert_array_almost_equal(mdkiF.smt2f, AWFgt)
assert_array_almost_equal(mdkiF.smt2di, DIgt)
assert_array_almost_equal(mdkiF.smt2uFA[MD > 0], uFAgt)
mask = MKgt_multi > 0
AWF = awf_from_msk(MKgt_multi, mask=mask)
assert_array_almost_equal(AWF, AWFgt)
```

## Next Steps


---

*Source: test_msdki.py:268 | Complexity: Advanced | Last updated: 2026-05-18*