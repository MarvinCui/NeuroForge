# How To: Qti Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the QTI model class.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test the QTI model class.'

```python
'Test the QTI model class.'
```

**Verification:**
```python
assert_warns(UserWarning, qti.QtiModel, gtab)
```

### Step 2: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(np.ones(1), bvecs=np.array([[1, 0, 0]]))
```

### Step 3: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.QtiModel, gtab)
```

### Step 4: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(np.ones(1), bvecs=np.array([[1, 0, 0]]), btens='LTE')
```

### Step 5: Call assert_warns()

```python
assert_warns(UserWarning, qti.QtiModel, gtab)
```

### Step 6: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, qti.QtiModel, _qti_gtab(rng), fit_method='non-linear')
```

### Step 7: Assign gtab = _qti_gtab(...)

```python
gtab = _qti_gtab(rng)
```

### Step 8: Assign qtimodel = qti.QtiModel(...)

```python
qtimodel = qti.QtiModel(gtab)
```

### Step 9: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(qtimodel.X, qti.design_matrix(gtab.btens))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test the QTI model class.'
gtab = gradient_table(np.ones(1), bvecs=np.array([[1, 0, 0]]))
npt.assert_raises(ValueError, qti.QtiModel, gtab)
gtab = gradient_table(np.ones(1), bvecs=np.array([[1, 0, 0]]), btens='LTE')
assert_warns(UserWarning, qti.QtiModel, gtab)
npt.assert_raises(ValueError, qti.QtiModel, _qti_gtab(rng), fit_method='non-linear')
gtab = _qti_gtab(rng)
qtimodel = qti.QtiModel(gtab)
npt.assert_almost_equal(qtimodel.X, qti.design_matrix(gtab.btens))
```

## Next Steps


---

*Source: test_qti.py:468 | Complexity: Advanced | Last updated: 2026-05-18*