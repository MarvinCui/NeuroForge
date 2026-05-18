# How To: Assert Logprob

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test assert logprob

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.raise_op`
- `scipy`
- `pymc.distributions`
- `pymc.logprob.basic`
- `tests.distributions.test_multivariate`


## Step-by-Step Guide

### Step 1: Assign rv = pt.random.normal(...)

```python
rv = pt.random.normal()
```

**Verification:**
```python
assert_op = Assert('Test assert')
```

### Step 2: Assign assert_op = Assert(...)

```python
assert_op = Assert('Test assert')
```

**Verification:**
```python
assert_rv = assert_op(rv, rv > 0)
```

### Step 3: Assign assert_rv = assert_op(...)

```python
assert_rv = assert_op(rv, rv > 0)
```

**Verification:**
```python
assert_rv.name = 'assert_rv'
```

### Step 4: Assign assert_rv.name = 'assert_rv'

```python
assert_rv.name = 'assert_rv'
```

**Verification:**
```python
assert_vv = assert_rv.clone()
```

### Step 5: Assign assert_vv = assert_rv.clone(...)

```python
assert_vv = assert_rv.clone()
```

**Verification:**
```python
assert_logp = conditional_logp({assert_rv: assert_vv})[assert_vv]
```

### Step 6: Assign assert_logp = value

```python
assert_logp = conditional_logp({assert_rv: assert_vv})[assert_vv]
```

**Verification:**
```python
assert_logp.eval({assert_vv: -5.0})
```

### Step 7: Assign valid_value = 3.0

```python
valid_value = 3.0
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(assert_logp.eval({assert_vv: valid_value}), stats.norm.logpdf(valid_value))
```

### Step 9: Call assert_logp.eval()

```python
assert_logp.eval({assert_vv: -5.0})
```


## Complete Example

```python
# Workflow
rv = pt.random.normal()
assert_op = Assert('Test assert')
assert_rv = assert_op(rv, rv > 0)
assert_rv.name = 'assert_rv'
assert_vv = assert_rv.clone()
assert_logp = conditional_logp({assert_rv: assert_vv})[assert_vv]
valid_value = 3.0
np.testing.assert_allclose(assert_logp.eval({assert_vv: valid_value}), stats.norm.logpdf(valid_value))
with pytest.raises(AssertionError, match='Test assert'):
    assert_logp.eval({assert_vv: -5.0})
```

## Next Steps


---

*Source: test_checks.py:80 | Complexity: Advanced | Last updated: 2026-05-18*