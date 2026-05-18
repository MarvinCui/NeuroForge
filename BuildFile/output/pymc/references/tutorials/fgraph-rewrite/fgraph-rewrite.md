# How To: Fgraph Rewrite

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test we can apply a simple rewrite to a PyMC Model.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.tensor.exceptions`
- `pymc`
- `pymc.distributions.shape_utils`
- `pymc.model.fgraph`

**Setup Required:**
```python
# Fixtures: non_centered_rewrite
```

## Step-by-Step Guide

### Step 1: 'Test we can apply a simple rewrite to a PyMC Model.'

```python
'Test we can apply a simple rewrite to a PyMC Model.'
```

**Verification:**
```python
assert m_new.named_vars_to_dims == {'subject_mean': ['subject'], 'subject_mean_raw_': ['subject'], 'obs': ['subject']}
```

### Step 2: Assign unknown = fgraph_from_model(...)

```python
fg, _ = fgraph_from_model(m_old)
```

**Verification:**
```python
assert set(m_new.named_vars) == {'group_mean', 'group_std', 'subject_mean_raw_', 'subject_mean', 'obs'}
```

### Step 3: Call non_centered_rewrite.apply()

```python
non_centered_rewrite.apply(fg)
```

**Verification:**
```python
assert {rv.name for rv in m_new.free_RVs} == {'group_mean', 'group_std', 'subject_mean_raw_'}
```

### Step 4: Assign m_new = model_from_fgraph(...)

```python
m_new = model_from_fgraph(fg)
```

**Verification:**
```python
assert {rv.name for rv in m_new.observed_RVs} == {'obs'}
```

### Step 5: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(pm.draw(m_new['subject_mean_raw_'], draws=7, random_seed=1), pm.draw(m_ref['subject_mean_raw_'], draws=7, random_seed=1))
```

**Verification:**
```python
assert {rv.name for rv in m_new.deterministics} == {'subject_mean'}
```

### Step 6: Assign ip = m_new.initial_point(...)

```python
ip = m_new.initial_point()
```

### Step 7: Call np.testing.assert_equal()

```python
np.testing.assert_equal(m_new.compile_logp()(ip), m_ref.compile_logp()(ip))
```

### Step 8: Assign group_mean = pm.Normal(...)

```python
group_mean = pm.Normal('group_mean')
```

### Step 9: Assign group_std = pm.HalfNormal(...)

```python
group_std = pm.HalfNormal('group_std')
```

### Step 10: Assign subject_mean = pm.Normal(...)

```python
subject_mean = pm.Normal('subject_mean', group_mean, group_std, dims=('subject',))
```

### Step 11: Assign obs = pm.Normal(...)

```python
obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10), dims=('subject',))
```

### Step 12: Assign group_mean = pm.Normal(...)

```python
group_mean = pm.Normal('group_mean')
```

### Step 13: Assign group_std = pm.HalfNormal(...)

```python
group_std = pm.HalfNormal('group_std')
```

### Step 14: Assign subject_mean_raw = pm.Normal(...)

```python
subject_mean_raw = pm.Normal('subject_mean_raw_', 0, 1, shape=(10,))
```

### Step 15: Assign subject_mean = pm.Deterministic(...)

```python
subject_mean = pm.Deterministic('subject_mean', group_mean + subject_mean_raw * group_std)
```

### Step 16: Assign obs = pm.Normal(...)

```python
obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10))
```


## Complete Example

```python
# Setup
# Fixtures: non_centered_rewrite

# Workflow
'Test we can apply a simple rewrite to a PyMC Model.'
with pm.Model(coords={'subject': range(10)}) as m_old:
    group_mean = pm.Normal('group_mean')
    group_std = pm.HalfNormal('group_std')
    subject_mean = pm.Normal('subject_mean', group_mean, group_std, dims=('subject',))
    obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10), dims=('subject',))
fg, _ = fgraph_from_model(m_old)
non_centered_rewrite.apply(fg)
m_new = model_from_fgraph(fg)
assert m_new.named_vars_to_dims == {'subject_mean': ['subject'], 'subject_mean_raw_': ['subject'], 'obs': ['subject']}
assert set(m_new.named_vars) == {'group_mean', 'group_std', 'subject_mean_raw_', 'subject_mean', 'obs'}
assert {rv.name for rv in m_new.free_RVs} == {'group_mean', 'group_std', 'subject_mean_raw_'}
assert {rv.name for rv in m_new.observed_RVs} == {'obs'}
assert {rv.name for rv in m_new.deterministics} == {'subject_mean'}
with pm.Model() as m_ref:
    group_mean = pm.Normal('group_mean')
    group_std = pm.HalfNormal('group_std')
    subject_mean_raw = pm.Normal('subject_mean_raw_', 0, 1, shape=(10,))
    subject_mean = pm.Deterministic('subject_mean', group_mean + subject_mean_raw * group_std)
    obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10))
np.testing.assert_array_equal(pm.draw(m_new['subject_mean_raw_'], draws=7, random_seed=1), pm.draw(m_ref['subject_mean_raw_'], draws=7, random_seed=1))
ip = m_new.initial_point()
np.testing.assert_equal(m_new.compile_logp()(ip), m_ref.compile_logp()(ip))
```

## Next Steps


---

*Source: test_fgraph.py:341 | Complexity: Advanced | Last updated: 2026-05-18*