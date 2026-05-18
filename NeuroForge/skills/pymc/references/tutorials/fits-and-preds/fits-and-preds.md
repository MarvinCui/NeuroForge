# How To: Fits And Preds

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Get MAP estimate for GP approximation, compare results and predictions to what's returned
by an unapproximated GP.  The tolerances are fairly wide, but narrow relative to initial
values of the unknown parameters.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `operator`
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.math`

**Setup Required:**
```python
# Fixtures: approx
```

## Step-by-Step Guide

### Step 1: "Get MAP estimate for GP approximation, compare results and predictions to what's returned\n        by an unapproximated GP.  The tolerances are fairly wide, but narrow relative to initial\n        values of the unknown parameters.\n        "

```python
"Get MAP estimate for GP approximation, compare results and predictions to what's returned\n        by an unapproximated GP.  The tolerances are fairly wide, but narrow relative to initial\n        values of the unknown parameters.\n        "
```

### Step 2: Call npt.assert_allclose()

```python
npt.assert_allclose(self.map_full['c'], map_approx['c'], atol=0.01, rtol=0.1)
```

### Step 3: Call npt.assert_allclose()

```python
npt.assert_allclose(self.map_full['sigma'], map_approx['sigma'], atol=0.01, rtol=0.1)
```

### Step 4: Call npt.assert_allclose()

```python
npt.assert_allclose(self.pred_mu, pred_mu_approx, atol=0.0, rtol=0.1)
```

### Step 5: Call npt.assert_allclose()

```python
npt.assert_allclose(self.pred_var, pred_var_approx, atol=0.0, rtol=0.1)
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(self.pred_mu, pred_mu_approx, atol=0.0, rtol=0.1)
```

### Step 7: Call npt.assert_allclose()

```python
npt.assert_allclose(self.pred_var, pred_var_approx, atol=0.0, rtol=0.1)
```

### Step 8: Assign cov_func = pm.gp.cov.Linear(...)

```python
cov_func = pm.gp.cov.Linear(1, c=0.0)
```

### Step 9: Assign c = pm.Normal(...)

```python
c = pm.Normal('c', mu=20.0, sigma=100.0, initval=-500.0)
```

### Step 10: Assign mean_func = pm.gp.mean.Constant(...)

```python
mean_func = pm.gp.mean.Constant(c)
```

### Step 11: Assign gp = pm.gp.MarginalApprox(...)

```python
gp = pm.gp.MarginalApprox(mean_func=mean_func, cov_func=cov_func, approx=approx)
```

### Step 12: Assign sigma = pm.HalfNormal(...)

```python
sigma = pm.HalfNormal('sigma', sigma=100, initval=50.0)
```

### Step 13: Call gp.marginal_likelihood()

```python
gp.marginal_likelihood('lik', self.x[:, None], self.x[:, None], self.y, sigma)
```

### Step 14: Assign map_approx = pm.find_MAP(...)

```python
map_approx = pm.find_MAP(method='bfgs')
```

### Step 15: Assign unknown = gp.predict(...)

```python
pred_mu_approx, pred_var_approx = gp.predict(self.x_new[:, None], point=map_approx, pred_noise=True, diag=True)
```

### Step 16: Assign unknown = gp.predict(...)

```python
pred_mu_approx, pred_var_approx = gp.predict(self.x_new[:, None], point=map_approx, pred_noise=True, diag=True)
```


## Complete Example

```python
# Setup
# Fixtures: approx

# Workflow
"Get MAP estimate for GP approximation, compare results and predictions to what's returned\n        by an unapproximated GP.  The tolerances are fairly wide, but narrow relative to initial\n        values of the unknown parameters.\n        "
with pm.Model() as model:
    cov_func = pm.gp.cov.Linear(1, c=0.0)
    c = pm.Normal('c', mu=20.0, sigma=100.0, initval=-500.0)
    mean_func = pm.gp.mean.Constant(c)
    gp = pm.gp.MarginalApprox(mean_func=mean_func, cov_func=cov_func, approx=approx)
    sigma = pm.HalfNormal('sigma', sigma=100, initval=50.0)
    gp.marginal_likelihood('lik', self.x[:, None], self.x[:, None], self.y, sigma)
    map_approx = pm.find_MAP(method='bfgs')
npt.assert_allclose(self.map_full['c'], map_approx['c'], atol=0.01, rtol=0.1)
npt.assert_allclose(self.map_full['sigma'], map_approx['sigma'], atol=0.01, rtol=0.1)
with model:
    pred_mu_approx, pred_var_approx = gp.predict(self.x_new[:, None], point=map_approx, pred_noise=True, diag=True)
npt.assert_allclose(self.pred_mu, pred_mu_approx, atol=0.0, rtol=0.1)
npt.assert_allclose(self.pred_var, pred_var_approx, atol=0.0, rtol=0.1)
with model:
    pred_mu_approx, pred_var_approx = gp.predict(self.x_new[:, None], point=map_approx, pred_noise=True, diag=True)
npt.assert_allclose(self.pred_mu, pred_mu_approx, atol=0.0, rtol=0.1)
npt.assert_allclose(self.pred_var, pred_var_approx, atol=0.0, rtol=0.1)
```

## Next Steps


---

*Source: test_gp.py:61 | Complexity: Advanced | Last updated: 2026-05-18*