# How To: Switch Mixture Measurable Cond Fails

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that logprob inference fails when the switch condition is an unvalued measurable variable.

Otherwise, the logp function would have to marginalize over this variable.

NOTE: This could be supported in the future, in which case this test can be removed/adapted

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.ifelse`
- `pytensor.link.numba`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.shape`
- `pytensor.tensor.subtensor`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.mixture`
- `pymc.logprob.rewriting`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: 'Test that logprob inference fails when the switch condition is an unvalued measurable variable.\n\n    Otherwise, the logp function would have to marginalize over this variable.\n\n    NOTE: This could be supported in the future, in which case this test can be removed/adapted\n    '

```python
'Test that logprob inference fails when the switch condition is an unvalued measurable variable.\n\n    Otherwise, the logp function would have to marginalize over this variable.\n\n    NOTE: This could be supported in the future, in which case this test can be removed/adapted\n    '
```

### Step 2: Assign cond_var = value

```python
cond_var = 1 - pt.random.bernoulli(p=0.5)
```

### Step 3: Assign true_branch = pt.random.normal(...)

```python
true_branch = pt.random.normal()
```

### Step 4: Assign false_branch = pt.random.normal(...)

```python
false_branch = pt.random.normal()
```

### Step 5: Assign switch = pt.switch(...)

```python
switch = pt.switch(cond_var, true_branch, false_branch)
```

### Step 6: Call logp()

```python
logp(switch, switch.type())
```


## Complete Example

```python
# Workflow
'Test that logprob inference fails when the switch condition is an unvalued measurable variable.\n\n    Otherwise, the logp function would have to marginalize over this variable.\n\n    NOTE: This could be supported in the future, in which case this test can be removed/adapted\n    '
cond_var = 1 - pt.random.bernoulli(p=0.5)
true_branch = pt.random.normal()
false_branch = pt.random.normal()
switch = pt.switch(cond_var, true_branch, false_branch)
with pytest.raises(NotImplementedError, match='Logprob method not implemented for'):
    logp(switch, switch.type())
```

## Next Steps


---

*Source: test_mixture.py:914 | Complexity: Intermediate | Last updated: 2026-05-18*