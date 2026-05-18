# How To: Special Log Exp Transforms

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test special log exp transforms

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.special`
- `pytensor.graph.basic`
- `pymc.distributions.continuous`
- `pymc.distributions.discrete`
- `pymc.logprob.basic`
- `pymc.logprob.transforms`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.distributions.test_transform`

**Setup Required:**
```python
# Fixtures: canonical_func, raw_func
```

## Step-by-Step Guide

### Step 1: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(name='base_rv')
```

**Verification:**
```python
assert equal_computations([logp_test], [logp_ref])
```

### Step 2: Assign vv = pt.scalar(...)

```python
vv = pt.scalar('vv')
```

### Step 3: Assign transformed_rv = raw_func(...)

```python
transformed_rv = raw_func(base_rv)
```

### Step 4: Assign ref_transformed_rv = canonical_func(...)

```python
ref_transformed_rv = canonical_func(base_rv)
```

### Step 5: Assign logp_test = logp(...)

```python
logp_test = logp(transformed_rv, vv)
```

### Step 6: Assign logp_ref = logp(...)

```python
logp_ref = logp(ref_transformed_rv, vv)
```

### Step 7: Assign vv_test = np.array(...)

```python
vv_test = np.array(0.25)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_ref.eval({vv: vv_test}), logp_test.eval({vv: vv_test}))
```

**Verification:**
```python
assert equal_computations([logp_test], [logp_ref])
```


## Complete Example

```python
# Setup
# Fixtures: canonical_func, raw_func

# Workflow
base_rv = pt.random.normal(name='base_rv')
vv = pt.scalar('vv')
transformed_rv = raw_func(base_rv)
ref_transformed_rv = canonical_func(base_rv)
logp_test = logp(transformed_rv, vv)
logp_ref = logp(ref_transformed_rv, vv)
if canonical_func in (pt.log2, pt.log10):
    vv_test = np.array(0.25)
    np.testing.assert_allclose(logp_ref.eval({vv: vv_test}), logp_test.eval({vv: vv_test}))
else:
    assert equal_computations([logp_test], [logp_ref])
```

## Next Steps


---

*Source: test_transforms.py:615 | Complexity: Advanced | Last updated: 2026-05-18*