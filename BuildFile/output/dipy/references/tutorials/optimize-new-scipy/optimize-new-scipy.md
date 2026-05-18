# How To: Optimize New Scipy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test optimize new scipy

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.sparse`
- `dipy.core.optimize`
- `dipy.core.optimize`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign opt = Optimizer(...)

```python
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='Powell')
```

### Step 2: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
```

### Step 3: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(opt.fopt, 0)
```

### Step 4: Assign opt = Optimizer(...)

```python
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08})
```

### Step 5: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(opt.fopt, 0)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(opt.evolution, None)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(opt.evolution, None)
```

### Step 9: Assign opt = Optimizer(...)

```python
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08}, evolution=False)
```

### Step 10: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
```

### Step 11: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(opt.fopt, 0)
```

### Step 12: Call opt.print_summary()

```python
opt.print_summary()
```

### Step 13: Assign opt = Optimizer(...)

```python
opt = Optimizer(fun=func2, x0=np.array([1.0, 1.0, 1.0, 5.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08}, evolution=True)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(opt.evolution.shape, (opt.nit, 4))
```

### Step 15: Assign opt = Optimizer(...)

```python
opt = Optimizer(fun=func2, x0=np.array([1.0, 1.0, 1.0, 5.0]), method='Powell', options={'xtol': 1e-06, 'ftol': 1e-06, 'maxiter': 1000000.0}, evolution=True)
```

### Step 16: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0, 0.0]))
```


## Complete Example

```python
# Workflow
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='Powell')
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
npt.assert_almost_equal(opt.fopt, 0)
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08})
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
npt.assert_almost_equal(opt.fopt, 0)
npt.assert_equal(opt.evolution, None)
npt.assert_equal(opt.evolution, None)
opt = Optimizer(fun=func, x0=np.array([1.0, 1.0, 1.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08}, evolution=False)
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0]))
npt.assert_almost_equal(opt.fopt, 0)
opt.print_summary()
opt = Optimizer(fun=func2, x0=np.array([1.0, 1.0, 1.0, 5.0]), method='L-BFGS-B', options={'maxcor': 10, 'ftol': 1e-07, 'gtol': 1e-05, 'eps': 1e-08}, evolution=True)
npt.assert_equal(opt.evolution.shape, (opt.nit, 4))
opt = Optimizer(fun=func2, x0=np.array([1.0, 1.0, 1.0, 5.0]), method='Powell', options={'xtol': 1e-06, 'ftol': 1e-06, 'maxiter': 1000000.0}, evolution=True)
npt.assert_array_almost_equal(opt.xopt, np.array([0, 0, 0, 0.0]))
```

## Next Steps


---

*Source: test_optimize.py:18 | Complexity: Advanced | Last updated: 2026-05-18*