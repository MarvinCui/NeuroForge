# How To: Scan Multiple Output Types

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test we can derive the logp for a scan that contains recurring and non-recurring measurable outputs.

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.raise_op`
- `pytensor.scan.utils`
- `scipy`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.scan`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test we can derive the logp for a scan that contains recurring and non-recurring measurable outputs.'

```python
'Test we can derive the logp for a scan that contains recurring and non-recurring measurable outputs.'
```

**Verification:**
```python
assert_no_rvs([xs_logp, ys_logp, zs_logp])
```

### Step 2: Assign unknown = pytensor.scan(...)

```python
xs, ys, zs = pytensor.scan(fn=lambda x_mu, y_tm1, z_tm2, z_tm1: (pt.random.normal(x_mu), pt.random.normal(y_tm1), pt.random.normal(z_tm1) + z_tm2), sequences=[pt.arange(10)], outputs_info=[None, pt.zeros(()), {'initial': pt.ones(2), 'taps': [-2, -1]}], return_updates=False)
```

### Step 3: Assign xs.name = 'xs'

```python
xs.name = 'xs'
```

### Step 4: Assign xs_value = xs.clone(...)

```python
xs_value = xs.clone()
```

### Step 5: Assign ys.name = 'ys'

```python
ys.name = 'ys'
```

### Step 6: Assign ys_value = ys.clone(...)

```python
ys_value = ys.clone()
```

### Step 7: Assign zs.name = 'zs'

```python
zs.name = 'zs'
```

### Step 8: Assign zs_value = zs.clone(...)

```python
zs_value = zs.clone()
```

### Step 9: Assign logp_dict = conditional_logp(...)

```python
logp_dict = conditional_logp({xs: xs_value, ys: ys_value, zs: zs_value})
```

### Step 10: Assign xs_logp = value

```python
xs_logp = logp_dict[xs_value]
```

### Step 11: Assign ys_logp = value

```python
ys_logp = logp_dict[ys_value]
```

### Step 12: Assign zs_logp = value

```python
zs_logp = logp_dict[zs_value]
```

### Step 13: Call assert_no_rvs()

```python
assert_no_rvs([xs_logp, ys_logp, zs_logp])
```

### Step 14: Assign fn = pytensor.function(...)

```python
fn = pytensor.function([xs_value, ys_value, zs_value], [xs_logp, ys_logp, zs_logp])
```

### Step 15: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(577)
```

### Step 16: Assign test_value = rng.uniform(...)

```python
test_value = rng.uniform(size=(10,))
```

### Step 17: Assign unknown = fn(...)

```python
xs_logp_eval, ys_logp_eval, zs_logp_eval = fn(test_value, test_value, test_value)
```

### Step 18: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(xs_logp_eval, stats.norm.logpdf(test_value, np.arange(10)))
```

### Step 19: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(ys_logp_eval, stats.norm.logpdf(test_value, [0, *test_value[:-1]]))
```

### Step 20: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(zs_logp_eval, stats.norm.logpdf(test_value, [a + b for a, b in itertools.pairwise([1, 1, *test_value[:-1]])]))
```


## Complete Example

```python
# Workflow
'Test we can derive the logp for a scan that contains recurring and non-recurring measurable outputs.'
xs, ys, zs = pytensor.scan(fn=lambda x_mu, y_tm1, z_tm2, z_tm1: (pt.random.normal(x_mu), pt.random.normal(y_tm1), pt.random.normal(z_tm1) + z_tm2), sequences=[pt.arange(10)], outputs_info=[None, pt.zeros(()), {'initial': pt.ones(2), 'taps': [-2, -1]}], return_updates=False)
xs.name = 'xs'
xs_value = xs.clone()
ys.name = 'ys'
ys_value = ys.clone()
zs.name = 'zs'
zs_value = zs.clone()
logp_dict = conditional_logp({xs: xs_value, ys: ys_value, zs: zs_value})
xs_logp = logp_dict[xs_value]
ys_logp = logp_dict[ys_value]
zs_logp = logp_dict[zs_value]
assert_no_rvs([xs_logp, ys_logp, zs_logp])
fn = pytensor.function([xs_value, ys_value, zs_value], [xs_logp, ys_logp, zs_logp])
rng = np.random.default_rng(577)
test_value = rng.uniform(size=(10,))
xs_logp_eval, ys_logp_eval, zs_logp_eval = fn(test_value, test_value, test_value)
np.testing.assert_allclose(xs_logp_eval, stats.norm.logpdf(test_value, np.arange(10)))
np.testing.assert_allclose(ys_logp_eval, stats.norm.logpdf(test_value, [0, *test_value[:-1]]))
np.testing.assert_allclose(zs_logp_eval, stats.norm.logpdf(test_value, [a + b for a, b in itertools.pairwise([1, 1, *test_value[:-1]])]))
```

## Next Steps


---

*Source: test_scan.py:518 | Complexity: Advanced | Last updated: 2026-05-18*