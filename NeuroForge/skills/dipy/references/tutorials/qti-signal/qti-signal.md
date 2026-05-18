# How To: Qti Signal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test QTI signal generation.

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

### Step 1: 'Test QTI signal generation.'

```python
'Test QTI signal generation.'
```

### Step 2: Assign bvals = np.ones(...)

```python
bvals = np.ones(6)
```

### Step 3: Assign phi = value

```python
phi = (1 + np.sqrt(5)) / 2
```

### Step 4: Assign bvecs = value

```python
bvecs = np.array([[0, 1, phi], [0, 1, -phi], [1, phi, 0], [1, -phi, 0], [phi, 0, 1], [phi, 0, -1]]) / np.linalg.norm([0, 1, phi])
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(6))
```

### Step 7: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs, btens='LTE')
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(2), np.eye(6))
```

### Step 9: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(5))
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.stack((np.eye(3), np.eye(3))), np.eye(5))
```

### Step 11: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3)[np.newaxis, :], np.eye(6))
```

### Step 12: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(6), S0=np.ones(2))
```

### Step 13: Call qti.qti_signal()

```python
qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), np.zeros((5, 6)), np.zeros((5, 21)))
```

### Step 14: Assign D = np.eye(...)

```python
D = np.eye(3)
```

### Step 15: Assign C = np.zeros(...)

```python
C = np.zeros((6, 6))
```

### Step 16: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), np.ones(6) * np.exp(-1))
```

### Step 17: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='PTE'), D, C))
```

### Step 18: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='STE'), D, C))
```

### Step 19: Assign DTD = _anisotropic_DTD(...)

```python
DTD = _anisotropic_DTD()
```

### Step 20: Assign D = np.mean(...)

```python
D = np.mean(DTD, axis=0)
```

### Step 21: Assign C = qti.dtd_covariance(...)

```python
C = qti.dtd_covariance(DTD)
```

### Step 22: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), np.ones(6) * 0.7490954)
```

### Step 23: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='PTE'), D, C), np.ones(6) * 0.72453716)
```

### Step 24: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='STE'), D, C), np.ones(6) * 0.71653131)
```


## Complete Example

```python
# Workflow
'Test QTI signal generation.'
bvals = np.ones(6)
phi = (1 + np.sqrt(5)) / 2
bvecs = np.array([[0, 1, phi], [0, 1, -phi], [1, phi, 0], [1, -phi, 0], [phi, 0, 1], [phi, 0, -1]]) / np.linalg.norm([0, 1, phi])
gtab = gradient_table(bvals, bvecs=bvecs)
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(6))
gtab = gradient_table(bvals, bvecs=bvecs, btens='LTE')
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(2), np.eye(6))
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(5))
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.stack((np.eye(3), np.eye(3))), np.eye(5))
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3)[np.newaxis, :], np.eye(6))
npt.assert_raises(ValueError, qti.qti_signal, gtab, np.eye(3), np.eye(6), S0=np.ones(2))
qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), np.zeros((5, 6)), np.zeros((5, 21)))
D = np.eye(3)
C = np.zeros((6, 6))
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), np.ones(6) * np.exp(-1))
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='PTE'), D, C))
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='STE'), D, C))
DTD = _anisotropic_DTD()
D = np.mean(DTD, axis=0)
C = qti.dtd_covariance(DTD)
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='LTE'), D, C), np.ones(6) * 0.7490954)
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='PTE'), D, C), np.ones(6) * 0.72453716)
npt.assert_almost_equal(qti.qti_signal(gradient_table(bvals, bvecs=bvecs, btens='STE'), D, C), np.ones(6) * 0.71653131)
```

## Next Steps


---

*Source: test_qti.py:193 | Complexity: Advanced | Last updated: 2026-05-18*