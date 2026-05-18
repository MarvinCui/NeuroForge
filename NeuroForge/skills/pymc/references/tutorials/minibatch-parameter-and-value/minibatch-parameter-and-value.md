# How To: Minibatch Parameter And Value

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test minibatch parameter and value

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `pymc`
- `pymc`
- `pymc.data`
- `pymc.variational.minibatch_rv`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(161)
```

**Verification:**
```python
assert logp_fn(ip) != logp_fn(ip)
```

### Step 2: Assign total_size = 1000

```python
total_size = 1000
```

### Step 3: Assign logp_fn = m.compile_logp(...)

```python
logp_fn = m.compile_logp()
```

### Step 4: Assign ip = m.initial_point(...)

```python
ip = m.initial_point()
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(ip), st.norm.logpdf(0) * 1000)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_fn(ip), st.norm.logpdf(1) * 1000)
```

**Verification:**
```python
assert logp_fn(ip) != logp_fn(ip)
```

### Step 7: Assign AD = pm.Data(...)

```python
AD = pm.Data('AD', np.arange(total_size, dtype='float64'))
```

### Step 8: Assign TD = pm.Data(...)

```python
TD = pm.Data('TD', np.arange(total_size, dtype='float64'))
```

### Step 9: Assign unknown = Minibatch(...)

```python
AD_mt, TD_mt = Minibatch(AD, TD, batch_size=9)
```

### Step 10: Call pm.Normal()

```python
pm.Normal('AD_predicted', mu=TD_mt, observed=AD_mt, total_size=1000)
```

### Step 11: Call pm.set_data()

```python
pm.set_data({'AD': np.arange(total_size) + 1})
```

### Step 12: Call pm.set_data()

```python
pm.set_data({'AD': rng.normal(size=1000)})
```


## Complete Example

```python
# Workflow
rng = np.random.default_rng(161)
total_size = 1000
with pm.Model(check_bounds=False) as m:
    AD = pm.Data('AD', np.arange(total_size, dtype='float64'))
    TD = pm.Data('TD', np.arange(total_size, dtype='float64'))
    AD_mt, TD_mt = Minibatch(AD, TD, batch_size=9)
    pm.Normal('AD_predicted', mu=TD_mt, observed=AD_mt, total_size=1000)
logp_fn = m.compile_logp()
ip = m.initial_point()
np.testing.assert_allclose(logp_fn(ip), st.norm.logpdf(0) * 1000)
with m:
    pm.set_data({'AD': np.arange(total_size) + 1})
np.testing.assert_allclose(logp_fn(ip), st.norm.logpdf(1) * 1000)
with m:
    pm.set_data({'AD': rng.normal(size=1000)})
assert logp_fn(ip) != logp_fn(ip)
```

## Next Steps


---

*Source: test_minibatch_rv.py:123 | Complexity: Advanced | Last updated: 2026-05-18*