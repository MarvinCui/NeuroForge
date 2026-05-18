# How To: List Mvnormals Logp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test list mvnormals logp

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytensor.tensor.random.op`
- `scipy.special`
- `pymc.distributions`
- `pymc.distributions.mixture`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.math`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.step_methods`
- `pymc.testing`
- `pymc.vartypes`


## Step-by-Step Guide

### Step 1: Assign mu1 = np.asarray(...)

```python
mu1 = np.asarray([0.0, 1.0])
```

**Verification:**
```python
assert_allclose(model.compile_logp(y, sum=False)(testpoint)[0], mixlogp_st)
```

### Step 2: Assign cov1 = np.diag(...)

```python
cov1 = np.diag([1.5, 2.5])
```

**Verification:**
```python
assert_allclose(model.compile_logp()(testpoint), mixlogp_st.sum() + priorlogp)
```

### Step 3: Assign mu2 = np.asarray(...)

```python
mu2 = np.asarray([1.0, 0.0])
```

### Step 4: Assign cov2 = np.diag(...)

```python
cov2 = np.diag([2.5, 3.5])
```

### Step 5: Assign obs = np.asarray(...)

```python
obs = np.asarray([[0.5, 0.5], mu1, mu2])
```

### Step 6: Assign complogp_st = value

```python
complogp_st = np.vstack((st.multivariate_normal.logpdf(obs, mu1, cov1), st.multivariate_normal.logpdf(obs, mu2, cov2))).T
```

### Step 7: Assign testpoint = model.initial_point(...)

```python
testpoint = model.initial_point()
```

### Step 8: Assign mixlogp_st = logsumexp(...)

```python
mixlogp_st = logsumexp(np.log(testpoint['w']) + complogp_st, axis=-1, keepdims=False)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(model.compile_logp(y, sum=False)(testpoint)[0], mixlogp_st)
```

### Step 10: Assign priorlogp = st.dirichlet.logpdf(...)

```python
priorlogp = st.dirichlet.logpdf(x=testpoint['w'], alpha=np.ones(2))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(model.compile_logp()(testpoint), mixlogp_st.sum() + priorlogp)
```

### Step 12: Assign w = Dirichlet(...)

```python
w = Dirichlet('w', floatX(np.ones(2)), default_transform=None, shape=(2,))
```

### Step 13: Assign mvncomp1 = MvNormal.dist(...)

```python
mvncomp1 = MvNormal.dist(mu=mu1, cov=cov1)
```

### Step 14: Assign mvncomp2 = MvNormal.dist(...)

```python
mvncomp2 = MvNormal.dist(mu=mu2, cov=cov2)
```

### Step 15: Assign y = Mixture(...)

```python
y = Mixture('x_obs', w, [mvncomp1, mvncomp2], observed=obs)
```


## Complete Example

```python
# Workflow
mu1 = np.asarray([0.0, 1.0])
cov1 = np.diag([1.5, 2.5])
mu2 = np.asarray([1.0, 0.0])
cov2 = np.diag([2.5, 3.5])
obs = np.asarray([[0.5, 0.5], mu1, mu2])
with Model() as model:
    w = Dirichlet('w', floatX(np.ones(2)), default_transform=None, shape=(2,))
    mvncomp1 = MvNormal.dist(mu=mu1, cov=cov1)
    mvncomp2 = MvNormal.dist(mu=mu2, cov=cov2)
    y = Mixture('x_obs', w, [mvncomp1, mvncomp2], observed=obs)
complogp_st = np.vstack((st.multivariate_normal.logpdf(obs, mu1, cov1), st.multivariate_normal.logpdf(obs, mu2, cov2))).T
testpoint = model.initial_point()
mixlogp_st = logsumexp(np.log(testpoint['w']) + complogp_st, axis=-1, keepdims=False)
assert_allclose(model.compile_logp(y, sum=False)(testpoint)[0], mixlogp_st)
priorlogp = st.dirichlet.logpdf(x=testpoint['w'], alpha=np.ones(2))
assert_allclose(model.compile_logp()(testpoint), mixlogp_st.sum() + priorlogp)
```

## Next Steps


---

*Source: test_mixture.py:429 | Complexity: Advanced | Last updated: 2026-05-18*