# How To: Check Parameters Can Be Replaced By Ninf

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test check parameters can be replaced by ninf

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pandas`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.sparse`
- `pytensor`
- `pytensor.compile`
- `pytensor.compile.builders`
- `pytensor.graph.basic`
- `pytensor.link.vm`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.data`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`
- `pymc.exceptions`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.vartypes`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign expr = pt.vector(...)

```python
expr = pt.vector('expr', shape=(3,))
```

### Step 2: Assign cond = pt.ge(...)

```python
cond = pt.ge(expr, 0)
```

### Step 3: Assign final_expr = check_parameters(...)

```python
final_expr = check_parameters(expr, cond, can_be_replaced_by_ninf=True)
```

### Step 4: Assign fn = compile(...)

```python
fn = compile([expr], final_expr)
```

### Step 5: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(fn(expr=[1, 2, 3]), [1, 2, 3])
```

### Step 6: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(fn(expr=[-1, 2, 3]), [-np.inf, -np.inf, -np.inf])
```

### Step 7: Assign final_expr = check_parameters(...)

```python
final_expr = check_parameters(expr, cond, msg='test', can_be_replaced_by_ninf=False)
```

### Step 8: Assign fn = compile(...)

```python
fn = compile([expr], final_expr)
```

### Step 9: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(fn(expr=[1, 2, 3]), [1, 2, 3])
```

### Step 10: Call fn()

```python
fn([-1, 2, 3])
```


## Complete Example

```python
# Workflow
expr = pt.vector('expr', shape=(3,))
cond = pt.ge(expr, 0)
final_expr = check_parameters(expr, cond, can_be_replaced_by_ninf=True)
fn = compile([expr], final_expr)
np.testing.assert_array_equal(fn(expr=[1, 2, 3]), [1, 2, 3])
np.testing.assert_array_equal(fn(expr=[-1, 2, 3]), [-np.inf, -np.inf, -np.inf])
final_expr = check_parameters(expr, cond, msg='test', can_be_replaced_by_ninf=False)
fn = compile([expr], final_expr)
np.testing.assert_array_equal(fn(expr=[1, 2, 3]), [1, 2, 3])
with pytest.raises(ParameterValueError, match='test'):
    fn([-1, 2, 3])
```

## Next Steps


---

*Source: test_pytensorf.py:309 | Complexity: Advanced | Last updated: 2026-05-18*