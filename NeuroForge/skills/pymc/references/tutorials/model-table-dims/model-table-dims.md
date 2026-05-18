# How To: Model Table Dims

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model table dims

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `pytensor.xtensor.type`
- `xarray`
- `pymc`
- `pymc`
- `pymc`
- `pymc.model.transform.optimization`
- `tests.test_printing`


## Step-by-Step Guide

### Step 1: Assign coords = value

```python
coords = {'subject': range(20), 'param': ['a', 'b']}
```

**Verification:**
```python
assert [s.rstrip() for s in text.splitlines()] == expected.splitlines()
```

### Step 2: Assign text = table_to_text(...)

```python
text = table_to_text(m.table())
```

### Step 3: Assign expected = '       Variable  Expression                             Dimensions\n───────────────────────────────────────────────────────────────────────────────\n            x =  Data                                   subject[20] × param[2]\n   y_obs_data =  Data                                   subject[20]\n\n         beta ~  Normal(0, 1)                           param[2]\n        sigma ~  HalfNormal(0, 1)\n          zsn ~  ZeroSumNormal(<constant>, <constant>)  subject[20]\n                                                        Parameter count = 23\n\n           mu =  f(beta, x)                             subject[20]\n\n beta_penalty =  Potential(f(beta))                     param[2]\n\n        y_obs ~  Normal(f(mu, zsn), sigma)              subject[20]\n'

```python
expected = '       Variable  Expression                             Dimensions\n───────────────────────────────────────────────────────────────────────────────\n            x =  Data                                   subject[20] × param[2]\n   y_obs_data =  Data                                   subject[20]\n\n         beta ~  Normal(0, 1)                           param[2]\n        sigma ~  HalfNormal(0, 1)\n          zsn ~  ZeroSumNormal(<constant>, <constant>)  subject[20]\n                                                        Parameter count = 23\n\n           mu =  f(beta, x)                             subject[20]\n\n beta_penalty =  Potential(f(beta))                     param[2]\n\n        y_obs ~  Normal(f(mu, zsn), sigma)              subject[20]\n'
```

**Verification:**
```python
assert [s.rstrip() for s in text.splitlines()] == expected.splitlines()
```

### Step 4: Assign x = pmd.Data(...)

```python
x = pmd.Data('x', np.random.normal(size=(20, 2)), dims=('subject', 'param'))
```

### Step 5: Assign y_obs_data = pmd.Data(...)

```python
y_obs_data = pmd.Data('y_obs_data', np.random.normal(size=(20,)), dims='subject')
```

### Step 6: Assign beta = pmd.Normal(...)

```python
beta = pmd.Normal('beta', mu=0, sigma=1, dims='param')
```

### Step 7: Assign mu = pmd.Deterministic(...)

```python
mu = pmd.Deterministic('mu', (x * beta).sum('param'))
```

### Step 8: Assign sigma = pmd.HalfNormal(...)

```python
sigma = pmd.HalfNormal('sigma', sigma=1)
```

### Step 9: Assign zsn = pmd.ZeroSumNormal(...)

```python
zsn = pmd.ZeroSumNormal('zsn', sigma=1.0, core_dims='subject')
```

### Step 10: Call pmd.Normal()

```python
pmd.Normal('y_obs', mu=mu + zsn, sigma=sigma, observed=y_obs_data)
```

### Step 11: Call pmd.Potential()

```python
pmd.Potential('beta_penalty', -beta)
```


## Complete Example

```python
# Workflow
coords = {'subject': range(20), 'param': ['a', 'b']}
with pm.Model(coords=coords) as m:
    x = pmd.Data('x', np.random.normal(size=(20, 2)), dims=('subject', 'param'))
    y_obs_data = pmd.Data('y_obs_data', np.random.normal(size=(20,)), dims='subject')
    beta = pmd.Normal('beta', mu=0, sigma=1, dims='param')
    mu = pmd.Deterministic('mu', (x * beta).sum('param'))
    sigma = pmd.HalfNormal('sigma', sigma=1)
    zsn = pmd.ZeroSumNormal('zsn', sigma=1.0, core_dims='subject')
    pmd.Normal('y_obs', mu=mu + zsn, sigma=sigma, observed=y_obs_data)
    pmd.Potential('beta_penalty', -beta)
text = table_to_text(m.table())
expected = '       Variable  Expression                             Dimensions\n───────────────────────────────────────────────────────────────────────────────\n            x =  Data                                   subject[20] × param[2]\n   y_obs_data =  Data                                   subject[20]\n\n         beta ~  Normal(0, 1)                           param[2]\n        sigma ~  HalfNormal(0, 1)\n          zsn ~  ZeroSumNormal(<constant>, <constant>)  subject[20]\n                                                        Parameter count = 23\n\n           mu =  f(beta, x)                             subject[20]\n\n beta_penalty =  Potential(f(beta))                     param[2]\n\n        y_obs ~  Normal(f(mu, zsn), sigma)              subject[20]\n'
assert [s.rstrip() for s in text.splitlines()] == expected.splitlines()
```

## Next Steps


---

*Source: test_model.py:266 | Complexity: Advanced | Last updated: 2026-05-18*