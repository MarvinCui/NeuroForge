# How To: Dtd Covariance

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test diffusion tensor distribution covariance calculation.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.qti`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: 'Test diffusion tensor distribution covariance calculation.'

```python
'Test diffusion tensor distribution covariance calculation.'
```

### Step 2: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.dtd_covariance, np.arange(2))
```

### Step 3: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.dtd_covariance, np.zeros((1, 1, 1)))
```

### Step 4: Assign DTD = _isotropic_DTD(...)

```python
DTD = _isotropic_DTD()
```

### Step 5: Assign C = np.zeros(...)

```python
C = np.zeros((6, 6))
```

### Step 6: Assign unknown = 0.98116667

```python
C[0:3, 0:3] = 0.98116667
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.dtd_covariance(DTD), C)
```

### Step 8: Assign DTD = _anisotropic_DTD(...)

```python
DTD = _anisotropic_DTD()
```

### Step 9: Assign C = value

```python
C = np.eye(6) * 2 / 15
```

### Step 10: Assign unknown = np.array(...)

```python
C[0:3, 0:3] = np.array([[4 / 45, -2 / 45, -2 / 45], [-2 / 45, 4 / 45, -2 / 45], [-2 / 45, -2 / 45, 4 / 45]])
```

### Step 11: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.dtd_covariance(DTD), C)
```


## Complete Example

```python
# Workflow
'Test diffusion tensor distribution covariance calculation.'
npt.assert_raises(ValueError, qti.dtd_covariance, np.arange(2))
npt.assert_raises(ValueError, qti.dtd_covariance, np.zeros((1, 1, 1)))
DTD = _isotropic_DTD()
C = np.zeros((6, 6))
C[0:3, 0:3] = 0.98116667
npt.assert_almost_equal(qti.dtd_covariance(DTD), C)
DTD = _anisotropic_DTD()
C = np.eye(6) * 2 / 15
C[0:3, 0:3] = np.array([[4 / 45, -2 / 45, -2 / 45], [-2 / 45, 4 / 45, -2 / 45], [-2 / 45, -2 / 45, 4 / 45]])
npt.assert_almost_equal(qti.dtd_covariance(DTD), C)
```

## Next Steps


---

*Source: test_qti.py:167 | Complexity: Advanced | Last updated: 2026-05-18*