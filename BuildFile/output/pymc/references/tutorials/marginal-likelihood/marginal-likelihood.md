# How To: Marginal Likelihood

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Verifies that the log marginal likelihood function
can be correctly computed for a Beta-Bernoulli model.

## Prerequisites

**Required Modules:**
- `logging`
- `warnings`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.stats`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.base`
- `pymc.distributions.transforms`
- `pymc.pytensorf`
- `pymc.smc.kernels`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: '\n        Verifies that the log marginal likelihood function\n        can be correctly computed for a Beta-Bernoulli model.\n        '

```python
'\n        Verifies that the log marginal likelihood function\n        can be correctly computed for a Beta-Bernoulli model.\n        '
```

**Verification:**
```python
assert abs(np.exp(marginals[1] - marginals[0]) - 4.0) <= 1
```

### Step 2: Assign data = np.repeat(...)

```python
data = np.repeat([1, 0], [50, 50])
```

### Step 3: Assign marginals = value

```python
marginals = []
```

### Step 4: Assign unknown = value

```python
a_prior_0, b_prior_0 = (1.0, 1.0)
```

### Step 5: Assign unknown = value

```python
a_prior_1, b_prior_1 = (20.0, 20.0)
```

**Verification:**
```python
assert abs(np.exp(marginals[1] - marginals[0]) - 4.0) <= 1
```

### Step 6: Assign lml = np.mean(...)

```python
lml = np.mean([chain[-1] for chain in trace.report.log_marginal_likelihood])
```

### Step 7: Call marginals.append()

```python
marginals.append(lml)
```

### Step 8: Assign a = pm.Beta(...)

```python
a = pm.Beta('a', alpha, beta)
```

### Step 9: Assign y = pm.Bernoulli(...)

```python
y = pm.Bernoulli('y', a, observed=data)
```

### Step 10: Assign trace = pm.sample_smc(...)

```python
trace = pm.sample_smc(2000, chains=2, return_inferencedata=False)
```


## Complete Example

```python
# Workflow
'\n        Verifies that the log marginal likelihood function\n        can be correctly computed for a Beta-Bernoulli model.\n        '
data = np.repeat([1, 0], [50, 50])
marginals = []
a_prior_0, b_prior_0 = (1.0, 1.0)
a_prior_1, b_prior_1 = (20.0, 20.0)
for alpha, beta in ((a_prior_0, b_prior_0), (a_prior_1, b_prior_1)):
    with pm.Model() as model:
        a = pm.Beta('a', alpha, beta)
        y = pm.Bernoulli('y', a, observed=data)
        trace = pm.sample_smc(2000, chains=2, return_inferencedata=False)
    lml = np.mean([chain[-1] for chain in trace.report.log_marginal_likelihood])
    marginals.append(lml)
assert abs(np.exp(marginals[1] - marginals[0]) - 4.0) <= 1
```

## Next Steps


---

*Source: test_smc.py:151 | Complexity: Advanced | Last updated: 2026-05-18*