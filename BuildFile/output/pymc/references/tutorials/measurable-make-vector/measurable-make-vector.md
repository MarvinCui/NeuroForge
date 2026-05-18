# How To: Measurable Make Vector

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test measurable make vector

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
base1_rv = pt.random.normal(name='base1')
```

**Verification:**
```python
assert make_vector_logp_eval.shape == y_testval.shape
```

### Step 2: Assign base2_rv = pt.random.halfnormal(...)

```python
base2_rv = pt.random.halfnormal(name='base2')
```

**Verification:**
```python
assert np.isclose(make_vector_logp_eval.sum(), ref_logp_eval_eval)
```

### Step 3: Assign base3_rv = pt.random.exponential(...)

```python
base3_rv = pt.random.exponential(name='base3')
```

### Step 4: Assign y_rv = pt.stack(...)

```python
y_rv = pt.stack((base1_rv, base2_rv, base3_rv))
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

### Step 8: Assign base3_vv = base3_rv.clone(...)

```python
base3_vv = base3_rv.clone()
```

### Step 9: Assign y_vv = y_rv.clone(...)

```python
y_vv = y_rv.clone()
```

### Step 10: Assign ref_logp = conditional_logp(...)

```python
ref_logp = conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv, base3_rv: base3_vv})
```

### Step 11: Assign ref_logp_combined = pt.sum(...)

```python
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
```

### Step 12: Assign make_vector_logp = logp(...)

```python
make_vector_logp = logp(y_rv, y_vv)
```

### Step 13: Assign base1_testval = base1_rv.eval(...)

```python
base1_testval = base1_rv.eval()
```

### Step 14: Assign base2_testval = base2_rv.eval(...)

```python
base2_testval = base2_rv.eval()
```

### Step 15: Assign base3_testval = base3_rv.eval(...)

```python
base3_testval = base3_rv.eval()
```

### Step 16: Assign y_testval = np.stack(...)

```python
y_testval = np.stack((base1_testval, base2_testval, base3_testval))
```

### Step 17: Assign ref_logp_eval_eval = ref_logp_combined.eval(...)

```python
ref_logp_eval_eval = ref_logp_combined.eval({base1_vv: base1_testval, base2_vv: base2_testval, base3_vv: base3_testval})
```

### Step 18: Assign make_vector_logp_eval = make_vector_logp.eval(...)

```python
make_vector_logp_eval = make_vector_logp.eval({y_vv: y_testval})
```

**Verification:**
```python
assert make_vector_logp_eval.shape == y_testval.shape
```


## Complete Example

```python
# Workflow
base1_rv = pt.random.normal(name='base1')
base2_rv = pt.random.halfnormal(name='base2')
base3_rv = pt.random.exponential(name='base3')
y_rv = pt.stack((base1_rv, base2_rv, base3_rv))
y_rv.name = 'y'
base1_vv = base1_rv.clone()
base2_vv = base2_rv.clone()
base3_vv = base3_rv.clone()
y_vv = y_rv.clone()
ref_logp = conditional_logp({base1_rv: base1_vv, base2_rv: base2_vv, base3_rv: base3_vv})
ref_logp_combined = pt.sum([pt.sum(factor) for factor in ref_logp.values()])
make_vector_logp = logp(y_rv, y_vv)
base1_testval = base1_rv.eval()
base2_testval = base2_rv.eval()
base3_testval = base3_rv.eval()
y_testval = np.stack((base1_testval, base2_testval, base3_testval))
ref_logp_eval_eval = ref_logp_combined.eval({base1_vv: base1_testval, base2_vv: base2_testval, base3_vv: base3_testval})
make_vector_logp_eval = make_vector_logp.eval({y_vv: y_testval})
assert make_vector_logp_eval.shape == y_testval.shape
assert np.isclose(make_vector_logp_eval.sum(), ref_logp_eval_eval)
```

## Next Steps


---

*Source: test_tensor.py:73 | Complexity: Advanced | Last updated: 2026-05-18*