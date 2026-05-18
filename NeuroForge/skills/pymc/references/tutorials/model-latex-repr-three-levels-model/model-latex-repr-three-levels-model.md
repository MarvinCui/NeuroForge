# How To: Model Latex Repr Three Levels Model

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model latex repr three levels model

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor.tensor.random`
- `rich.console`
- `rich.table`
- `pymc`
- `pymc`
- `pymc.distributions`
- `pymc.math`
- `pymc.model`
- `pymc.printing`
- `pymc.pytensorf`
- `pymc.printing`
- `pymc.dims.distributions`
- `pymc.dims.distributions`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign latex_repr = censored_model.str_repr(...)

```python
latex_repr = censored_model.str_repr(formatting='latex')
```

**Verification:**
```python
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

### Step 2: Assign expected = value

```python
expected = ['$$', '\\begin{array}{rcl}', '\\text{mu} &\\sim & \\operatorname{Normal}(0,~5)\\\\\\text{sigma} &\\sim & \\operatorname{HalfCauchy}(2.5)\\\\\\text{censored\\_normal} &\\sim & \\operatorname{Censored}(\\operatorname{Normal}(\\text{mu},~\\text{sigma}),~-2,~2)', '\\end{array}', '$$']
```

**Verification:**
```python
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

### Step 3: Assign mu = Normal(...)

```python
mu = Normal('mu', 0.0, 5.0)
```

### Step 4: Assign sigma = HalfCauchy(...)

```python
sigma = HalfCauchy('sigma', 2.5)
```

### Step 5: Assign normal_dist = Normal.dist(...)

```python
normal_dist = Normal.dist(mu=mu, sigma=sigma)
```

### Step 6: Assign censored_normal = Censored(...)

```python
censored_normal = Censored('censored_normal', normal_dist, lower=-2.0, upper=2.0, observed=[1, 0, 0.5])
```


## Complete Example

```python
# Workflow
with Model() as censored_model:
    mu = Normal('mu', 0.0, 5.0)
    sigma = HalfCauchy('sigma', 2.5)
    normal_dist = Normal.dist(mu=mu, sigma=sigma)
    censored_normal = Censored('censored_normal', normal_dist, lower=-2.0, upper=2.0, observed=[1, 0, 0.5])
latex_repr = censored_model.str_repr(formatting='latex')
expected = ['$$', '\\begin{array}{rcl}', '\\text{mu} &\\sim & \\operatorname{Normal}(0,~5)\\\\\\text{sigma} &\\sim & \\operatorname{HalfCauchy}(2.5)\\\\\\text{censored\\_normal} &\\sim & \\operatorname{Censored}(\\operatorname{Normal}(\\text{mu},~\\text{sigma}),~-2,~2)', '\\end{array}', '$$']
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

## Next Steps


---

*Source: test_printing.py:263 | Complexity: Intermediate | Last updated: 2026-05-18*