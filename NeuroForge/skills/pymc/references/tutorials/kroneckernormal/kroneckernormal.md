# How To: Kroneckernormal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test kroneckernormal

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `warnings`
- `numpy`
- `numpy.random`
- `numpy.testing`
- `pytensor`
- `pytest`
- `scipy.special`
- `scipy.stats`
- `pytensor`
- `pytensor.compile.mode`
- `pytensor.tensor`
- `pytensor.tensor.blockwise`
- `pytensor.tensor.linalg.decomposition.cholesky`
- `pytensor.tensor.linalg.inverse`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.random.utils`
- `pymc`
- `pymc`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.utils`
- `pymc.math`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.testing`

**Setup Required:**
```python
# Fixtures: n, m, sigma
```

## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(5)
```

### Step 2: Assign N = value

```python
N = n * m
```

### Step 3: Assign covs = value

```python
covs = [RandomPdMatrix(n), RandomPdMatrix(m)]
```

### Step 4: Assign chols = list(...)

```python
chols = list(map(np.linalg.cholesky, covs))
```

### Step 5: Assign evds = list(...)

```python
evds = list(map(np.linalg.eigh, covs))
```

### Step 6: Assign dom = Domain(...)

```python
dom = Domain([np.random.randn(N) * 0.1], edges=(None, None), shape=N)
```

### Step 7: Assign mu = Domain(...)

```python
mu = Domain([np.random.randn(N) * 0.1], edges=(None, None), shape=N)
```

### Step 8: Assign std_args = value

```python
std_args = {'mu': mu}
```

### Step 9: Assign cov_args = value

```python
cov_args = {'covs': covs}
```

### Step 10: Assign chol_args = value

```python
chol_args = {'chols': chols}
```

### Step 11: Assign evd_args = value

```python
evd_args = {'evds': evds}
```

### Step 12: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_cov, extra_args=cov_args, scipy_args=cov_args)
```

### Step 13: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_chol, extra_args=chol_args, scipy_args=chol_args)
```

### Step 14: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_evd, extra_args=evd_args, scipy_args=evd_args)
```

### Step 15: Assign dom = Domain(...)

```python
dom = Domain([np.random.randn(2, N) * 0.1], edges=(None, None), shape=(2, N))
```

### Step 16: Assign unknown = 2

```python
cov_args['size'] = 2
```

### Step 17: Assign unknown = 2

```python
chol_args['size'] = 2
```

### Step 18: Assign unknown = 2

```python
evd_args['size'] = 2
```

### Step 19: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_cov, extra_args=cov_args, scipy_args=cov_args)
```

### Step 20: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_chol, extra_args=chol_args, scipy_args=chol_args)
```

### Step 21: Call check_logp()

```python
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_evd, extra_args=evd_args, scipy_args=evd_args)
```

### Step 22: Assign unknown = Domain(...)

```python
std_args['sigma'] = Domain([sigma], edges=(None, None))
```

### Step 23: Assign unknown = sigma

```python
args['sigma'] = sigma
```


## Complete Example

```python
# Setup
# Fixtures: n, m, sigma

# Workflow
np.random.seed(5)
N = n * m
covs = [RandomPdMatrix(n), RandomPdMatrix(m)]
chols = list(map(np.linalg.cholesky, covs))
evds = list(map(np.linalg.eigh, covs))
dom = Domain([np.random.randn(N) * 0.1], edges=(None, None), shape=N)
mu = Domain([np.random.randn(N) * 0.1], edges=(None, None), shape=N)
std_args = {'mu': mu}
cov_args = {'covs': covs}
chol_args = {'chols': chols}
evd_args = {'evds': evds}
if sigma is not None and sigma != 0:
    std_args['sigma'] = Domain([sigma], edges=(None, None))
else:
    for args in [cov_args, chol_args, evd_args]:
        args['sigma'] = sigma
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_cov, extra_args=cov_args, scipy_args=cov_args)
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_chol, extra_args=chol_args, scipy_args=chol_args)
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_evd, extra_args=evd_args, scipy_args=evd_args)
dom = Domain([np.random.randn(2, N) * 0.1], edges=(None, None), shape=(2, N))
cov_args['size'] = 2
chol_args['size'] = 2
evd_args['size'] = 2
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_cov, extra_args=cov_args, scipy_args=cov_args)
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_chol, extra_args=chol_args, scipy_args=chol_args)
check_logp(pm.KroneckerNormal, dom, std_args, kron_normal_logpdf_evd, extra_args=evd_args, scipy_args=evd_args)
```

## Next Steps


---

*Source: test_multivariate.py:424 | Complexity: Advanced | Last updated: 2026-05-18*