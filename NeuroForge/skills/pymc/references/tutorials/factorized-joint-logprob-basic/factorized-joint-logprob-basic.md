# How To: Factorized Joint Logprob Basic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test factorized joint logprob basic

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
assert equal_computations([a_logp_comb], [a_logp_exp])
```

### Step 2: Assign a.name = 'a'

```python
a.name = 'a'
```

**Verification:**
```python
assert equal_computations([total_ll_combined], [total_ll_exp])
```

### Step 3: Assign a_value_var = a.clone(...)

```python
a_value_var = a.clone()
```

**Verification:**
```python
assert_no_rvs(b_logp_combined)
```

### Step 4: Assign a_logp = conditional_logp(...)

```python
a_logp = conditional_logp({a: a_value_var})
```

**Verification:**
```python
assert b_value_var in res_ancestors
```

### Step 5: Assign a_logp_comb = next(...)

```python
a_logp_comb = next(iter(a_logp.values()))
```

**Verification:**
```python
assert c_value_var in res_ancestors
```

### Step 6: Assign a_logp_exp = logp(...)

```python
a_logp_exp = logp(a, a_value_var)
```

**Verification:**
```python
assert a_value_var in res_ancestors
```

### Step 7: Assign sigma = pt.random.invgamma(...)

```python
sigma = pt.random.invgamma(0.5, 0.5)
```

### Step 8: Assign Y = pt.random.normal(...)

```python
Y = pt.random.normal(0.0, sigma)
```

### Step 9: Assign sigma_value_var = sigma.clone(...)

```python
sigma_value_var = sigma.clone()
```

### Step 10: Assign y_value_var = Y.clone(...)

```python
y_value_var = Y.clone()
```

### Step 11: Assign total_ll = conditional_logp(...)

```python
total_ll = conditional_logp({Y: y_value_var, sigma: sigma_value_var})
```

### Step 12: Assign total_ll_combined = pt.add(...)

```python
total_ll_combined = pt.add(*total_ll.values())
```

### Step 13: Assign ll_Y = logp(...)

```python
ll_Y = logp(Y, y_value_var)
```

### Step 14: Assign unknown = replace_rvs_by_values(...)

```python
ll_Y, = replace_rvs_by_values([ll_Y], rvs_to_values={sigma: sigma_value_var})
```

### Step 15: Assign total_ll_exp = value

```python
total_ll_exp = ll_Y + logp(sigma, sigma_value_var)
```

**Verification:**
```python
assert equal_computations([total_ll_combined], [total_ll_exp])
```

### Step 16: Assign c = pt.random.normal(...)

```python
c = pt.random.normal()
```

### Step 17: Assign c.name = 'c'

```python
c.name = 'c'
```

### Step 18: Assign b_l = value

```python
b_l = c * a + 2.0
```

### Step 19: Assign b = pt.random.uniform(...)

```python
b = pt.random.uniform(b_l, b_l + 1.0)
```

### Step 20: Assign b.name = 'b'

```python
b.name = 'b'
```

### Step 21: Assign b_value_var = b.clone(...)

```python
b_value_var = b.clone()
```

### Step 22: Assign c_value_var = c.clone(...)

```python
c_value_var = c.clone()
```

### Step 23: Assign b_logp = conditional_logp(...)

```python
b_logp = conditional_logp({a: a_value_var, b: b_value_var, c: c_value_var})
```

### Step 24: Assign b_logp_combined = pt.sum(...)

```python
b_logp_combined = pt.sum([pt.sum(factor) for factor in b_logp.values()])
```

### Step 25: Call assert_no_rvs()

```python
assert_no_rvs(b_logp_combined)
```

### Step 26: Assign res_ancestors = list(...)

```python
res_ancestors = list(ancestors((b_logp_combined,)))
```

**Verification:**
```python
assert b_value_var in res_ancestors
```


## Complete Example

```python
# Workflow
a = pt.random.uniform(0.0, 1.0)
a.name = 'a'
a_value_var = a.clone()
a_logp = conditional_logp({a: a_value_var})
a_logp_comb = next(iter(a_logp.values()))
a_logp_exp = logp(a, a_value_var)
assert equal_computations([a_logp_comb], [a_logp_exp])
sigma = pt.random.invgamma(0.5, 0.5)
Y = pt.random.normal(0.0, sigma)
sigma_value_var = sigma.clone()
y_value_var = Y.clone()
total_ll = conditional_logp({Y: y_value_var, sigma: sigma_value_var})
total_ll_combined = pt.add(*total_ll.values())
ll_Y = logp(Y, y_value_var)
ll_Y, = replace_rvs_by_values([ll_Y], rvs_to_values={sigma: sigma_value_var})
total_ll_exp = ll_Y + logp(sigma, sigma_value_var)
assert equal_computations([total_ll_combined], [total_ll_exp])
c = pt.random.normal()
c.name = 'c'
b_l = c * a + 2.0
b = pt.random.uniform(b_l, b_l + 1.0)
b.name = 'b'
b_value_var = b.clone()
c_value_var = c.clone()
b_logp = conditional_logp({a: a_value_var, b: b_value_var, c: c_value_var})
b_logp_combined = pt.sum([pt.sum(factor) for factor in b_logp.values()])
assert_no_rvs(b_logp_combined)
res_ancestors = list(ancestors((b_logp_combined,)))
assert b_value_var in res_ancestors
assert c_value_var in res_ancestors
assert a_value_var in res_ancestors
```

## Next Steps


---

*Source: test_basic.py:65 | Complexity: Advanced | Last updated: 2026-05-18*