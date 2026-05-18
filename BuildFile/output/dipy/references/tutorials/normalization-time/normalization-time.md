# How To: Normalization Time

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test normalization time

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign ut = 10

```python
ut = 10
```

**Verification:**
```python
assert_almost_equal(int0, 1.0)
```

### Step 2: Assign tmin = 0

```python
tmin = 0
```

**Verification:**
```python
assert_almost_equal(int1, 1.0)
```

### Step 3: Assign tmax = 100

```python
tmax = 100
```

**Verification:**
```python
assert_almost_equal(int2, 1.0)
```

### Step 4: Assign int0 = value

```python
int0 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(0, ut, t) * qtdmri.temporal_basis(0, ut, t), tmin, tmax)[0]
```

### Step 5: Assign int1 = value

```python
int1 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(1, ut, t) * qtdmri.temporal_basis(1, ut, t), tmin, tmax)[0]
```

### Step 6: Assign int2 = value

```python
int2 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(2, ut, t) * qtdmri.temporal_basis(2, ut, t), tmin, tmax)[0]
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(int0, 1.0)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(int1, 1.0)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(int2, 1.0)
```


## Complete Example

```python
# Workflow
ut = 10
tmin = 0
tmax = 100
int0 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(0, ut, t) * qtdmri.temporal_basis(0, ut, t), tmin, tmax)[0]
int1 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(1, ut, t) * qtdmri.temporal_basis(1, ut, t), tmin, tmax)[0]
int2 = integrate.quad(lambda t: qtdmri.qtdmri_temporal_normalization(ut) ** 2 * qtdmri.temporal_basis(2, ut, t) * qtdmri.temporal_basis(2, ut, t), tmin, tmax)[0]
assert_almost_equal(int0, 1.0)
assert_almost_equal(int1, 1.0)
assert_almost_equal(int2, 1.0)
```

## Next Steps


---

*Source: test_qtdmri.py:176 | Complexity: Advanced | Last updated: 2026-05-18*