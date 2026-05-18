# How To: Sfm Sklearnlinearsolver

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sfm sklearnlinearsolver

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.cross_validation`
- `dipy.reconst.sfm`
- `dipy.sims.voxel`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign unknown = dpd.get_fnames(...)

```python
fdata, fbvals, fbvecs = dpd.get_fnames()
```

### Step 2: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
```

### Step 3: Assign sfmodel = sfm.SparseFascicleModel(...)

```python
sfmodel = sfm.SparseFascicleModel(gtab, solver=SillySolver())
```

### Step 4: Call npt.assert_()

```python
npt.assert_(isinstance(sfmodel.solver, SillySolver))
```

### Step 5: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, sfm.SparseFascicleModel, gtab, solver=EvenSillierSolver())
```

### Step 6: Assign self.coef_ = np.ones(...)

```python
self.coef_ = np.ones(X.shape[-1])
```

### Step 7: Assign self.coef_ = np.ones(...)

```python
self.coef_ = np.ones(X.shape[-1])
```


## Complete Example

```python
# Workflow
class SillySolver(opt.SKLearnLinearSolver):

    def fit(self, X, y):
        self.coef_ = np.ones(X.shape[-1])

class EvenSillierSolver:

    def fit(self, X, y):
        self.coef_ = np.ones(X.shape[-1])
fdata, fbvals, fbvecs = dpd.get_fnames()
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
sfmodel = sfm.SparseFascicleModel(gtab, solver=SillySolver())
npt.assert_(isinstance(sfmodel.solver, SillySolver))
npt.assert_raises(ValueError, sfm.SparseFascicleModel, gtab, solver=EvenSillierSolver())
```

## Next Steps


---

*Source: test_sfm.py:177 | Complexity: Intermediate | Last updated: 2026-05-18*