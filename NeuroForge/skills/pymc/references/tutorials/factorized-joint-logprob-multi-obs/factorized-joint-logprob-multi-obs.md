# How To: Factorized Joint Logprob Multi Obs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test factorized joint logprob multi obs

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

### Step 1: Assign a = pt.random.uniform(...)

```python
a = pt.random.uniform(0.0, 1.0)
```

**Verification:**
```python
assert equal_computations([logp_res_combined], [logp_exp])
```

### Step 2: Assign b = pt.random.normal(...)

```python
b = pt.random.normal(0.0, 1.0)
```

**Verification:**
```python
assert equal_computations([logp_res_comb], [exp_logp_comb])
```

### Step 3: Assign a_val = a.clone(...)

```python
a_val = a.clone()
```

### Step 4: Assign b_val = b.clone(...)

```python
b_val = b.clone()
```

### Step 5: Assign logp_res = conditional_logp(...)

```python
logp_res = conditional_logp({a: a_val, b: b_val})
```

### Step 6: Assign logp_res_combined = pt.add(...)

```python
logp_res_combined = pt.add(*logp_res.values())
```

### Step 7: Assign logp_exp = value

```python
logp_exp = logp(a, a_val) + logp(b, b_val)
```

**Verification:**
```python
assert equal_computations([logp_res_combined], [logp_exp])
```

### Step 8: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(0, 1)
```

### Step 9: Assign y = pt.random.normal(...)

```python
y = pt.random.normal(x, 1)
```

### Step 10: Assign x_val = x.clone(...)

```python
x_val = x.clone()
```

### Step 11: Assign y_val = y.clone(...)

```python
y_val = y.clone()
```

### Step 12: Assign logp_res = conditional_logp(...)

```python
logp_res = conditional_logp({x: x_val, y: y_val})
```

### Step 13: Assign exp_logp = conditional_logp(...)

```python
exp_logp = conditional_logp({x: x_val, y: y_val})
```

### Step 14: Assign logp_res_comb = pt.sum(...)

```python
logp_res_comb = pt.sum([pt.sum(factor) for factor in logp_res.values()])
```

### Step 15: Assign exp_logp_comb = pt.sum(...)

```python
exp_logp_comb = pt.sum([pt.sum(factor) for factor in exp_logp.values()])
```

**Verification:**
```python
assert equal_computations([logp_res_comb], [exp_logp_comb])
```


## Complete Example

```python
# Workflow
a = pt.random.uniform(0.0, 1.0)
b = pt.random.normal(0.0, 1.0)
a_val = a.clone()
b_val = b.clone()
logp_res = conditional_logp({a: a_val, b: b_val})
logp_res_combined = pt.add(*logp_res.values())
logp_exp = logp(a, a_val) + logp(b, b_val)
assert equal_computations([logp_res_combined], [logp_exp])
x = pt.random.normal(0, 1)
y = pt.random.normal(x, 1)
x_val = x.clone()
y_val = y.clone()
logp_res = conditional_logp({x: x_val, y: y_val})
exp_logp = conditional_logp({x: x_val, y: y_val})
logp_res_comb = pt.sum([pt.sum(factor) for factor in logp_res.values()])
exp_logp_comb = pt.sum([pt.sum(factor) for factor in exp_logp.values()])
assert equal_computations([logp_res_comb], [exp_logp_comb])
```

## Next Steps


---

*Source: test_basic.py:121 | Complexity: Advanced | Last updated: 2026-05-18*