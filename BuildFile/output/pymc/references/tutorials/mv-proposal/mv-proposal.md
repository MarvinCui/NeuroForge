# How To: Mv Proposal

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mv proposal

## Prerequisites

**Required Modules:**
- `warnings`
- `arviz`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytest`
- `pytensor.compile.mode`
- `pymc`
- `pymc.step_methods.metropolis`
- `pymc.step_methods.state`
- `pymc.testing`
- `tests`
- `tests.helpers`
- `tests.models`


## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(42)
```

### Step 2: Assign cov = np.random.randn(...)

```python
cov = np.random.randn(5, 5)
```

### Step 3: Assign cov = cov.dot(...)

```python
cov = cov.dot(cov.T)
```

### Step 4: Assign prop = MultivariateNormalProposal(...)

```python
prop = MultivariateNormalProposal(cov)
```

### Step 5: Assign samples = np.array(...)

```python
samples = np.array([prop() for _ in range(10000)])
```

### Step 6: Call npt.assert_allclose()

```python
npt.assert_allclose(np.cov(samples.T), cov, rtol=0.2)
```


## Complete Example

```python
# Workflow
np.random.seed(42)
cov = np.random.randn(5, 5)
cov = cov.dot(cov.T)
prop = MultivariateNormalProposal(cov)
samples = np.array([prop() for _ in range(10000)])
npt.assert_allclose(np.cov(samples.T), cov, rtol=0.2)
```

## Next Steps


---

*Source: test_metropolis.py:82 | Complexity: Intermediate | Last updated: 2026-05-18*