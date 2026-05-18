# How To: Measurable Join With Constant Input

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test measurable join with constant input

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.tensor.random.type`
- `scipy`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign base1_rv = pt.random.normal(...)

```python
base1_rv = pt.random.normal(size=(2,), name='base1')
```

**Verification:**
```python
assert y_logp_eval.shape == y_testval.shape
```

### Step 2: Assign base2_rv = pt.random.exponential(...)

```python
base2_rv = pt.random.exponential(size=(3,), name='base2')
```

**Verification:**
```python
assert np.isclose(y_logp_eval.sum(), ref_logp_eval)
```

### Step 3: Assign const = pt.constant(...)

```python
const = pt.constant(np.array([0.0, 0.0, 0.0]))
```

**Verification:**
```python
assert y_logp_eval_bad[2] == -np.inf
```

### Step 4: Assign y_rv = pt.join(...)

```python
y_rv = pt.join(0, base1_rv, const, base2_rv)
```

### Step 5: Assign y_rv.name = 'y'

```python
y_rv.name = 'y'
```

### Step 6: Assign base1_vv = base1_rv.clone(...)

```python
base1_vv = base1_rv.clone()
```

### Step 7: Assign base2_vv = base2_rv.clone(...)

```python
base2_vv = base2_rv.clone()
```

### Step 8: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 9: Assign ref_logp = conditional_logp(...)

```python
ref_logp = conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv})
```

### Step 10: Assign ref_logp_combined = pt.sum(...)

```python
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
```

### Step 11: Assign y_logp = logp(...)

```python
y_logp = logp(y_rv, y_vv)
```

### Step 12: Assign base1_testval = base1_rv.eval(...)

```python
base1_testval = base1_rv.eval()
```

### Step 13: Assign base2_testval = base2_rv.eval(...)

```python
base2_testval = base2_rv.eval()
```

### Step 14: Assign y_testval = np.concatenate.astype(...)

```python
y_testval = np.concatenate([base1_testval, np.zeros(3), base2_testval]).astype(y_vv.dtype)
```

### Step 15: Assign ref_logp_eval = ref_logp_combined.eval(...)

```python
ref_logp_eval = ref_logp_combined.eval({base1_vv: base1_testval, base2_vv: base2_testval})
```

### Step 16: Assign y_logp_eval = y_logp.eval(...)

```python
y_logp_eval = y_logp.eval({y_vv: y_testval})
```

**Verification:**
```python
assert y_logp_eval.shape == y_testval.shape
```

### Step 17: Assign y_testval_bad = y_testval.copy(...)

```python
y_testval_bad = y_testval.copy()
```

### Step 18: Assign unknown = 1.0

```python
y_testval_bad[2] = 1.0
```

### Step 19: Assign y_logp_eval_bad = y_logp.eval(...)

```python
y_logp_eval_bad = y_logp.eval({y_vv: y_testval_bad})
```

**Verification:**
```python
assert y_logp_eval_bad[2] == -np.inf
```


## Complete Example

```python
# Workflow
base1_rv = pt.random.normal(size=(2,), name='base1')
base2_rv = pt.random.exponential(size=(3,), name='base2')
const = pt.constant(np.array([0.0, 0.0, 0.0]))
y_rv = pt.join(0, base1_rv, const, base2_rv)
y_rv.name = 'y'
base1_vv = base1_rv.clone()
base2_vv = base2_rv.clone()
y_vv = y_rv.clone()
ref_logp = conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv})
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
y_logp = logp(y_rv, y_vv)
base1_testval = base1_rv.eval()
base2_testval = base2_rv.eval()
y_testval = np.concatenate([base1_testval, np.zeros(3), base2_testval]).astype(y_vv.dtype)
ref_logp_eval = ref_logp_combined.eval({base1_vv: base1_testval, base2_vv: base2_testval})
y_logp_eval = y_logp.eval({y_vv: y_testval})
assert y_logp_eval.shape == y_testval.shape
assert np.isclose(y_logp_eval.sum(), ref_logp_eval)
y_testval_bad = y_testval.copy()
y_testval_bad[2] = 1.0
y_logp_eval_bad = y_logp.eval({y_vv: y_testval_bad})
assert y_logp_eval_bad[2] == -np.inf
```

## Next Steps


---

*Source: test_tensor.py:223 | Complexity: Advanced | Last updated: 2026-05-18*