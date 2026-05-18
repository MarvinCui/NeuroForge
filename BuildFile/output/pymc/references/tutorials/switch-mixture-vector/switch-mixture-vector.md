# How To: Switch Mixture Vector

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test switch mixture vector

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: switch_cond_scalar
```

## Step-by-Step Guide

### Step 1: Assign true_branch = pt.exp(...)

```python
true_branch = pt.exp(pt.random.normal(size=(4,)))
```

### Step 2: Assign false_branch = pt.abs(...)

```python
false_branch = pt.abs(pt.random.normal(size=(4,)))
```

### Step 3: Assign switch = pt.switch(...)

```python
switch = pt.switch(switch_cond, true_branch, false_branch)
```

### Step 4: Assign switch.name = 'switch_mix'

```python
switch.name = 'switch_mix'
```

### Step 5: Assign switch_value = switch.clone(...)

```python
switch_value = switch.clone()
```

### Step 6: Assign switch_logp = logp(...)

```python
switch_logp = logp(switch, switch_value)
```

### Step 7: Assign test_switch_value = np.linspace(...)

```python
test_switch_value = np.linspace(0.1, 2.5, 4)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(switch_logp.eval({switch_cond: test_switch_cond, switch_value: test_switch_value}), np.where(test_switch_cond, logp(true_branch, test_switch_value).eval(), logp(false_branch, test_switch_value).eval()))
```

### Step 9: Assign switch_cond = pt.scalar(...)

```python
switch_cond = pt.scalar('switch_cond', dtype=bool)
```

### Step 10: Assign switch_cond = pt.vector(...)

```python
switch_cond = pt.vector('switch_cond', dtype=bool)
```

### Step 11: Assign test_switch_cond = np.array(...)

```python
test_switch_cond = np.array(0, dtype=bool)
```

### Step 12: Assign test_switch_cond = np.array(...)

```python
test_switch_cond = np.array([0, 1, 0, 1], dtype=bool)
```


## Complete Example

```python
# Setup
# Fixtures: switch_cond_scalar

# Workflow
if switch_cond_scalar:
    switch_cond = pt.scalar('switch_cond', dtype=bool)
else:
    switch_cond = pt.vector('switch_cond', dtype=bool)
true_branch = pt.exp(pt.random.normal(size=(4,)))
false_branch = pt.abs(pt.random.normal(size=(4,)))
switch = pt.switch(switch_cond, true_branch, false_branch)
switch.name = 'switch_mix'
switch_value = switch.clone()
switch_logp = logp(switch, switch_value)
if switch_cond_scalar:
    test_switch_cond = np.array(0, dtype=bool)
else:
    test_switch_cond = np.array([0, 1, 0, 1], dtype=bool)
test_switch_value = np.linspace(0.1, 2.5, 4)
np.testing.assert_allclose(switch_logp.eval({switch_cond: test_switch_cond, switch_value: test_switch_value}), np.where(test_switch_cond, logp(true_branch, test_switch_value).eval(), logp(false_branch, test_switch_value).eval()))
```

## Next Steps


---

*Source: test_mixture.py:886 | Complexity: Advanced | Last updated: 2026-05-18*