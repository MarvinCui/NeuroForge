# How To: Model To Graphviz For Model With Data Container

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test model to graphviz for model with data container

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign exp_without = value

```python
exp_without = ['x [label="x\n~\\Data" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal"]', 'obs [label="obs\n~\nNormal" style=filled]']
```

**Verification:**
```python
assert expected in g.source
```

### Step 2: Assign exp_with = value

```python
exp_with = ['x [label="x\n~\nData" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal(mu=0.0, sigma=10.0)"]', f'obs [label="obs\n~\nNormal(mu=f(f(beta), x), sigma={obs_sigma})" style=filled]']
```

**Verification:**
```python
assert path.exists(tmp_path / 'model.png')
```

### Step 3: Call pm.model_to_graphviz()

```python
pm.model_to_graphviz(model, save=tmp_path / 'model.png')
```

**Verification:**
```python
assert path.exists(tmp_path / 'a_model.png')
```

### Step 4: Call pm.model_to_graphviz()

```python
pm.model_to_graphviz(model, save=tmp_path / 'a_model', dpi=100)
```

**Verification:**
```python
assert path.exists(tmp_path / 'a_model.png')
```

### Step 5: Assign x = pm.Data(...)

```python
x = pm.Data('x', [1.0, 2.0, 3.0])
```

### Step 6: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0])
```

### Step 7: Assign beta = pm.Normal(...)

```python
beta = pm.Normal('beta', 0, 10.0)
```

### Step 8: Assign obs_sigma = floatX(...)

```python
obs_sigma = floatX(np.sqrt(0.01))
```

### Step 9: Call pm.Normal()

```python
pm.Normal('obs', beta * x, obs_sigma, observed=y)
```

### Step 10: Call pm.sample()

```python
pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
```

### Step 11: Assign g = pm.model_to_graphviz(...)

```python
g = pm.model_to_graphviz(model, formatting=formatting)
```

### Step 12: Call pm.model_to_graphviz()

```python
pm.model_to_graphviz(model, formatting=formatting)
```

**Verification:**
```python
assert expected in g.source
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Data('y', [1.0, 2.0, 3.0])
    beta = pm.Normal('beta', 0, 10.0)
    obs_sigma = floatX(np.sqrt(0.01))
    pm.Normal('obs', beta * x, obs_sigma, observed=y)
    pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
for formatting in {'latex', 'latex_with_params'}:
    with pytest.raises(ValueError, match='Unsupported formatting'):
        pm.model_to_graphviz(model, formatting=formatting)
exp_without = ['x [label="x\n~\\Data" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal"]', 'obs [label="obs\n~\nNormal" style=filled]']
exp_with = ['x [label="x\n~\nData" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal(mu=0.0, sigma=10.0)"]', f'obs [label="obs\n~\nNormal(mu=f(f(beta), x), sigma={obs_sigma})" style=filled]']
for formatting, expected_substrings in [('plain', exp_without), ('plain_with_params', exp_with)]:
    g = pm.model_to_graphviz(model, formatting=formatting)
    for expected in expected_substrings:
        assert expected in g.source
pm.model_to_graphviz(model, save=tmp_path / 'model.png')
assert path.exists(tmp_path / 'model.png')
pm.model_to_graphviz(model, save=tmp_path / 'a_model', dpi=100)
assert path.exists(tmp_path / 'a_model.png')
```

## Next Steps


---

*Source: test_data.py:270 | Complexity: Advanced | Last updated: 2026-05-18*