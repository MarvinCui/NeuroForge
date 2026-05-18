# How To: Scan Over Seqs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that logprob inference for scans based on sequences (mapping).

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

### Step 1: 'Test that logprob inference for scans based on sequences (mapping).'

```python
'Test that logprob inference for scans based on sequences (mapping).'
```

**Verification:**
```python
assert_no_rvs(ys_logp)
```

### Step 2: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(543)
```

### Step 3: Assign n_steps = 10

```python
n_steps = 10
```

### Step 4: Assign xs = pt.random.normal(...)

```python
xs = pt.random.normal(size=(n_steps,), name='xs')
```

### Step 5: Assign ys = pytensor.scan(...)

```python
ys = pytensor.scan(fn=lambda x: pt.random.normal(x), sequences=[xs], outputs_info=[None], name='ys', return_updates=False)
```

### Step 6: Assign xs_vv = ys.clone(...)

```python
xs_vv = ys.clone()
```

### Step 7: Assign ys_vv = ys.clone(...)

```python
ys_vv = ys.clone()
```

### Step 8: Assign ys_logp = value

```python
ys_logp = conditional_logp({xs: xs_vv, ys: ys_vv})[ys_vv]
```

### Step 9: Call assert_no_rvs()

```python
assert_no_rvs(ys_logp)
```

### Step 10: Assign xs_test = rng.normal(...)

```python
xs_test = rng.normal(size=(10,))
```

### Step 11: Assign ys_test = rng.normal(...)

```python
ys_test = rng.normal(size=(10,))
```

### Step 12: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(ys_logp.eval({xs_vv: xs_test, ys_vv: ys_test}), stats.norm.logpdf(ys_test, xs_test))
```


## Complete Example

```python
# Workflow
'Test that logprob inference for scans based on sequences (mapping).'
rng = np.random.default_rng(543)
n_steps = 10
xs = pt.random.normal(size=(n_steps,), name='xs')
ys = pytensor.scan(fn=lambda x: pt.random.normal(x), sequences=[xs], outputs_info=[None], name='ys', return_updates=False)
xs_vv = ys.clone()
ys_vv = ys.clone()
ys_logp = conditional_logp({xs: xs_vv, ys: ys_vv})[ys_vv]
assert_no_rvs(ys_logp)
xs_test = rng.normal(size=(10,))
ys_test = rng.normal(size=(10,))
np.testing.assert_array_almost_equal(ys_logp.eval({xs_vv: xs_test, ys_vv: ys_test}), stats.norm.logpdf(ys_test, xs_test))
```

## Next Steps


---

*Source: test_scan.py:433 | Complexity: Advanced | Last updated: 2026-05-18*