# How To: Factorized Joint Logprob Diff Dims

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test factorized joint logprob diff dims

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.graph.basic`
- `pytensor.graph.traversal`
- `pytensor.tensor.random.op`
- `scipy`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign M = pt.matrix(...)

```python
M = pt.matrix('M')
```

**Verification:**
```python
assert exp_logp_val == pytest.approx(logp_val)
```

### Step 2: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(0, 1, size=M.shape[1], name='X')
```

### Step 3: Assign y = pt.random.normal(...)

```python
y = pt.random.normal(M.dot(x), 1, name='Y')
```

### Step 4: Assign x_vv = x.clone(...)

```python
x_vv = x.clone()
```

### Step 5: Assign x_vv.name = 'x'

```python
x_vv.name = 'x'
```

### Step 6: Assign y_vv = y.clone(...)

```python
y_vv = y.clone()
```

### Step 7: Assign y_vv.name = 'y'

```python
y_vv.name = 'y'
```

### Step 8: Assign logp = conditional_logp(...)

```python
logp = conditional_logp({x: x_vv, y: y_vv})
```

### Step 9: Assign logp_combined = pt.sum(...)

```python
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
```

### Step 10: Assign M_val = np.random.normal(...)

```python
M_val = np.random.normal(size=(10, 3))
```

### Step 11: Assign x_val = np.random.normal(...)

```python
x_val = np.random.normal(size=(3,))
```

### Step 12: Assign y_val = np.random.normal(...)

```python
y_val = np.random.normal(size=(10,))
```

### Step 13: Assign point = value

```python
point = {M: M_val, x_vv: x_val, y_vv: y_val}
```

### Step 14: Assign logp_val = logp_combined.eval(...)

```python
logp_val = logp_combined.eval(point)
```

### Step 15: Assign exp_logp_val = value

```python
exp_logp_val = sp.norm.logpdf(x_val, 0, 1).sum() + sp.norm.logpdf(y_val, M_val.dot(x_val), 1).sum()
```

**Verification:**
```python
assert exp_logp_val == pytest.approx(logp_val)
```


## Complete Example

```python
# Workflow
M = pt.matrix('M')
x = pt.random.normal(0, 1, size=M.shape[1], name='X')
y = pt.random.normal(M.dot(x), 1, name='Y')
x_vv = x.clone()
x_vv.name = 'x'
y_vv = y.clone()
y_vv.name = 'y'
logp = conditional_logp({x: x_vv, y: y_vv})
logp_combined = pt.sum([pt.sum(factor) for factor in logp.values()])
M_val = np.random.normal(size=(10, 3))
x_val = np.random.normal(size=(3,))
y_val = np.random.normal(size=(10,))
point = {M: M_val, x_vv: x_val, y_vv: y_val}
logp_val = logp_combined.eval(point)
exp_logp_val = sp.norm.logpdf(x_val, 0, 1).sum() + sp.norm.logpdf(y_val, M_val.dot(x_val), 1).sum()
assert exp_logp_val == pytest.approx(logp_val)
```

## Next Steps


---

*Source: test_basic.py:148 | Complexity: Advanced | Last updated: 2026-05-18*