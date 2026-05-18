# How To: Get Sampler Stats

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get sampler stats

## Prerequisites

**Required Modules:**
- `logging`
- `numpy`
- `pytest`
- `xarray`
- `pymc`
- `pymc.backends`
- `pymc.pytensorf`
- `pymc.step_methods`
- `pymc.step_methods.arraystep`
- `pymc.backends.mcbackend`
- `mcbackend`
- `mcbackend.npproto.utils`


## Step-by-Step Guide

### Step 1: Assign N = 45

```python
N = 45
```

**Verification:**
```python
assert isinstance(run, mcb.backends.numpy.NumPyRun)
```

### Step 2: Assign cra = value

```python
cra = traces[0]
```

**Verification:**
```python
assert isinstance(cra, ChainRecordAdapter)
```

### Step 3: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(2023)
```

**Verification:**
```python
assert len(cra) == N
```

### Step 4: Assign draws_a = cra.get_values(...)

```python
draws_a = cra.get_values('a')
```

**Verification:**
```python
assert point['a'] == draws_a[i]
```

### Step 5: Assign draws_b = cra.get_values(...)

```python
draws_b = cra.get_values('b')
```

**Verification:**
```python
assert point['b'] == draws_b[i]
```

### Step 6: Assign draws_c = cra.get_values(...)

```python
draws_c = cra.get_values('c')
```

**Verification:**
```python
assert point['c'] == draws_c[i]
```

### Step 7: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(draws_a + draws_b, draws_c)
```

**Verification:**
```python
assert s1.shape == (21,)
```

### Step 8: Assign i = np.random.randint(...)

```python
i = np.random.randint(0, N)
```

**Verification:**
```python
assert s1.dtype == np.dtype('float64')
```

### Step 9: Assign point = cra.point(...)

```python
point = cra.point(idx=i)
```

**Verification:**
```python
assert point['a'] == draws_a[i]
```

### Step 10: Assign s1 = cra.get_sampler_stats(...)

```python
s1 = cra.get_sampler_stats('s1', sampler_idx=None, burn=3, thin=2)
```

**Verification:**
```python
assert s1.shape == (21,)
```

### Step 11: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(s1, np.arange(N)[3:None:2])
```

### Step 12: Assign a = pm.Normal(...)

```python
a = pm.Normal('a')
```

### Step 13: Assign b = pm.Uniform(...)

```python
b = pm.Uniform('b')
```

### Step 14: Assign c = pm.Deterministic(...)

```python
c = pm.Deterministic('c', a + b)
```

### Step 15: Assign ip = pmodel.initial_point(...)

```python
ip = pmodel.initial_point()
```

### Step 16: Assign shared = make_shared_replacements(...)

```python
shared = make_shared_replacements(ip, [a, b], pmodel)
```

### Step 17: Assign unknown = init_traces(...)

```python
run, traces = init_traces(backend=mcb.NumPyBackend(), chains=1, expected_length=N, step=ToyStepper([a, b], shared), initial_point=pmodel.initial_point(), model=pmodel)
```

### Step 18: Assign draw = value

```python
draw = {'a': rng.normal(), 'b_interval__': rng.normal()}
```

### Step 19: Assign stats = value

```python
stats = [{'tune': i <= 5, 's1': i, 'accepted': bool(rng.randint(0, 2))}]
```

### Step 20: Call cra.record()

```python
cra.record(draw, stats, in_warmup=i <= 5)
```


## Complete Example

```python
# Workflow
N = 45
with pm.Model() as pmodel:
    a = pm.Normal('a')
    b = pm.Uniform('b')
    c = pm.Deterministic('c', a + b)
    ip = pmodel.initial_point()
    shared = make_shared_replacements(ip, [a, b], pmodel)
    run, traces = init_traces(backend=mcb.NumPyBackend(), chains=1, expected_length=N, step=ToyStepper([a, b], shared), initial_point=pmodel.initial_point(), model=pmodel)
cra = traces[0]
assert isinstance(run, mcb.backends.numpy.NumPyRun)
assert isinstance(cra, ChainRecordAdapter)
rng = np.random.RandomState(2023)
for i in range(N):
    draw = {'a': rng.normal(), 'b_interval__': rng.normal()}
    stats = [{'tune': i <= 5, 's1': i, 'accepted': bool(rng.randint(0, 2))}]
    cra.record(draw, stats, in_warmup=i <= 5)
assert len(cra) == N
draws_a = cra.get_values('a')
draws_b = cra.get_values('b')
draws_c = cra.get_values('c')
np.testing.assert_array_equal(draws_a + draws_b, draws_c)
i = np.random.randint(0, N)
point = cra.point(idx=i)
assert point['a'] == draws_a[i]
assert point['b'] == draws_b[i]
assert point['c'] == draws_c[i]
s1 = cra.get_sampler_stats('s1', sampler_idx=None, burn=3, thin=2)
assert s1.shape == (21,)
assert s1.dtype == np.dtype('float64')
np.testing.assert_array_equal(s1, np.arange(N)[3:None:2])
```

## Next Steps


---

*Source: test_mcbackend.py:181 | Complexity: Advanced | Last updated: 2026-05-18*