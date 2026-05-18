# How To: Orthogonality Temporal Basis Functions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test orthogonality temporal basis functions

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
assert_almost_equal(int1, 0.0)
```

### Step 2: Assign tmin = 0

```python
tmin = 0
```

**Verification:**
```python
assert_almost_equal(int2, 0.0)
```

### Step 3: Assign tmax = 100

```python
tmax = 100
```

**Verification:**
```python
assert_almost_equal(int3, 0.0)
```

### Step 4: Assign int1 = integrate.quad(...)

```python
int1 = integrate.quad(lambda t: qtdmri.temporal_basis(1, ut, t) * qtdmri.temporal_basis(2, ut, t), tmin, tmax)
```

**Verification:**
```python
assert_almost_equal(int4, 0.0)
```

### Step 5: Assign int2 = integrate.quad(...)

```python
int2 = integrate.quad(lambda t: qtdmri.temporal_basis(2, ut, t) * qtdmri.temporal_basis(3, ut, t), tmin, tmax)
```

### Step 6: Assign int3 = integrate.quad(...)

```python
int3 = integrate.quad(lambda t: qtdmri.temporal_basis(3, ut, t) * qtdmri.temporal_basis(4, ut, t), tmin, tmax)
```

### Step 7: Assign int4 = integrate.quad(...)

```python
int4 = integrate.quad(lambda t: qtdmri.temporal_basis(4, ut, t) * qtdmri.temporal_basis(5, ut, t), tmin, tmax)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(int1, 0.0)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(int2, 0.0)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(int3, 0.0)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(int4, 0.0)
```


## Complete Example

```python
# Workflow
ut = 10
tmin = 0
tmax = 100
int1 = integrate.quad(lambda t: qtdmri.temporal_basis(1, ut, t) * qtdmri.temporal_basis(2, ut, t), tmin, tmax)
int2 = integrate.quad(lambda t: qtdmri.temporal_basis(2, ut, t) * qtdmri.temporal_basis(3, ut, t), tmin, tmax)
int3 = integrate.quad(lambda t: qtdmri.temporal_basis(3, ut, t) * qtdmri.temporal_basis(4, ut, t), tmin, tmax)
int4 = integrate.quad(lambda t: qtdmri.temporal_basis(4, ut, t) * qtdmri.temporal_basis(5, ut, t), tmin, tmax)
assert_almost_equal(int1, 0.0)
assert_almost_equal(int2, 0.0)
assert_almost_equal(int3, 0.0)
assert_almost_equal(int4, 0.0)
```

## Next Steps


---

*Source: test_qtdmri.py:143 | Complexity: Advanced | Last updated: 2026-05-18*