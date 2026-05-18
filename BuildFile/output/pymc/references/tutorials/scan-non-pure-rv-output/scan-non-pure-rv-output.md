# How To: Scan Non Pure Rv Output

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test scan non pure rv output

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

### Step 1: Assign grw = pytensor.scan(...)

```python
grw = pytensor.scan(fn=lambda xtm1: pt.random.normal() + xtm1, outputs_info=[pt.zeros(())], n_steps=10, name='grw', return_updates=False)
```

**Verification:**
```python
assert_no_rvs(grw_logp)
```

### Step 2: Assign grw_vv = grw.clone(...)

```python
grw_vv = grw.clone()
```

### Step 3: Assign grw_logp = logp(...)

```python
grw_logp = logp(grw, grw_vv)
```

### Step 4: Call assert_no_rvs()

```python
assert_no_rvs(grw_logp)
```

### Step 5: Assign grw_vv_test = value

```python
grw_vv_test = np.arange(10) + 1
```

### Step 6: Call np.testing.assert_array_almost_equal()

```python
np.testing.assert_array_almost_equal(grw_logp.eval({grw_vv: grw_vv_test}), stats.norm.logpdf(np.ones(10)))
```


## Complete Example

```python
# Workflow
grw = pytensor.scan(fn=lambda xtm1: pt.random.normal() + xtm1, outputs_info=[pt.zeros(())], n_steps=10, name='grw', return_updates=False)
grw_vv = grw.clone()
grw_logp = logp(grw, grw_vv)
assert_no_rvs(grw_logp)
grw_vv_test = np.arange(10) + 1
np.testing.assert_array_almost_equal(grw_logp.eval({grw_vv: grw_vv_test}), stats.norm.logpdf(np.ones(10)))
```

## Next Steps


---

*Source: test_scan.py:413 | Complexity: Intermediate | Last updated: 2026-05-18*