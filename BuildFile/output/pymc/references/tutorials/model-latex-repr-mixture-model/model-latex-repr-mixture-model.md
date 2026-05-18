# How To: Model Latex Repr Mixture Model

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test model latex repr mixture model

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

### Step 1: Assign latex_repr = mix_model.str_repr(...)

```python
latex_repr = mix_model.str_repr(formatting='latex')
```

**Verification:**
```python
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

### Step 2: Assign expected = value

```python
expected = ['$$', '\\begin{array}{rcl}', '\\text{w} &\\sim & \\operatorname{Dirichlet}(\\text{<constant>})\\\\\\text{mix} &\\sim & \\operatorname{Mixture}(\\text{w},~\\operatorname{Normal}(0,~5),~\\operatorname{StudentT}(7,~0,~1))', '\\end{array}', '$$']
```

**Verification:**
```python
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

### Step 3: Assign w = Dirichlet(...)

```python
w = Dirichlet('w', [1, 1])
```

### Step 4: Assign mix = Mixture(...)

```python
mix = Mixture('mix', w=w, comp_dists=[Normal.dist(0.0, 5.0), StudentT.dist(7.0)])
```


## Complete Example

```python
# Workflow
with Model() as mix_model:
    w = Dirichlet('w', [1, 1])
    mix = Mixture('mix', w=w, comp_dists=[Normal.dist(0.0, 5.0), StudentT.dist(7.0)])
latex_repr = mix_model.str_repr(formatting='latex')
expected = ['$$', '\\begin{array}{rcl}', '\\text{w} &\\sim & \\operatorname{Dirichlet}(\\text{<constant>})\\\\\\text{mix} &\\sim & \\operatorname{Mixture}(\\text{w},~\\operatorname{Normal}(0,~5),~\\operatorname{StudentT}(7,~0,~1))', '\\end{array}', '$$']
assert [line.strip() for line in latex_repr.split('\n')] == expected
```

## Next Steps


---

*Source: test_printing.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*