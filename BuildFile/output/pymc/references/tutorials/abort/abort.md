# How To: Abort

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test abort

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `multiprocessing`
- `os`
- `platform`
- `sys`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.ops`
- `pytensor.tensor.type`
- `pymc`
- `pymc.sampling.parallel`
- `pymc.pytensorf`
- `pymc.step_methods`

**Setup Required:**
```python
# Fixtures: mp_start_method
```

## Step-by-Step Guide

### Step 1: Assign step = CompoundStep(...)

```python
step = CompoundStep([step1, step2])
```

### Step 2: Assign a = pm.Normal(...)

```python
a = pm.Normal('a', shape=1)
```

### Step 3: Assign b = pm.HalfNormal(...)

```python
b = pm.HalfNormal('b')
```

### Step 4: Assign step1 = pm.NUTS(...)

```python
step1 = pm.NUTS([model.rvs_to_values[a]])
```

### Step 5: Assign step2 = pm.Metropolis(...)

```python
step2 = pm.Metropolis([model.rvs_to_values[b]])
```

### Step 6: Assign step_method_pickled = cloudpickle.dumps(...)

```python
step_method_pickled = cloudpickle.dumps(step, protocol=-1)
```

### Step 7: Assign step_method_pickled = None

```python
step_method_pickled = None
```

### Step 8: Assign ctx = multiprocessing.get_context(...)

```python
ctx = multiprocessing.get_context(mp_start_method)
```

### Step 9: Assign proc = ps.ProcessAdapter(...)

```python
proc = ps.ProcessAdapter(10, 10, step, chain=3, seed=1, mp_ctx=ctx, start={'a': floatX(np.array([1.0])), 'b_log__': floatX(np.array(2.0))}, step_method_pickled=step_method_pickled)
```

### Step 10: Call proc.start()

```python
proc.start()
```

### Step 11: Call proc.join()

```python
proc.join()
```

### Step 12: Call proc.write_next()

```python
proc.write_next()
```

### Step 13: Assign out = ps.ProcessAdapter.recv_draw(...)

```python
out = ps.ProcessAdapter.recv_draw([proc])
```

### Step 14: Call proc.abort()

```python
proc.abort()
```


## Complete Example

```python
# Setup
# Fixtures: mp_start_method

# Workflow
with pm.Model() as model:
    a = pm.Normal('a', shape=1)
    b = pm.HalfNormal('b')
    step1 = pm.NUTS([model.rvs_to_values[a]])
    step2 = pm.Metropolis([model.rvs_to_values[b]])
step = CompoundStep([step1, step2])
if platform.system() == 'Windows' and mp_start_method == 'fork':
    return
if mp_start_method == 'spawn':
    step_method_pickled = cloudpickle.dumps(step, protocol=-1)
else:
    step_method_pickled = None
for abort in [False, True]:
    ctx = multiprocessing.get_context(mp_start_method)
    proc = ps.ProcessAdapter(10, 10, step, chain=3, seed=1, mp_ctx=ctx, start={'a': floatX(np.array([1.0])), 'b_log__': floatX(np.array(2.0))}, step_method_pickled=step_method_pickled)
    proc.start()
    while True:
        proc.write_next()
        out = ps.ProcessAdapter.recv_draw([proc])
        if out[1]:
            break
    if abort:
        proc.abort()
    proc.join()
```

## Next Steps


---

*Source: test_parallel.py:133 | Complexity: Advanced | Last updated: 2026-05-18*