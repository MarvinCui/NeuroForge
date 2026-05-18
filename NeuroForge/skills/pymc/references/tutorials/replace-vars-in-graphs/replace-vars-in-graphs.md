# How To: Replace Vars In Graphs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test replace vars in graphs

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

### Step 1: Assign inp = shared(...)

```python
inp = shared(0.0, name='inp')
```

**Verification:**
```python
assert x.eval() < 50
```

### Step 2: Assign x = pm.Normal.dist(...)

```python
x = pm.Normal.dist(inp)
```

**Verification:**
```python
assert new_x.eval() > 50
```

### Step 3: Assign replacements = value

```python
replacements = {inp: inp + 100}
```

### Step 4: Assign unknown = replace_vars_in_graphs(...)

```python
[new_x] = replace_vars_in_graphs([x], replacements=replacements)
```

**Verification:**
```python
assert x.eval() < 50
```


## Complete Example

```python
# Workflow
inp = shared(0.0, name='inp')
x = pm.Normal.dist(inp)
replacements = {inp: inp + 100}
[new_x] = replace_vars_in_graphs([x], replacements=replacements)
assert x.eval() < 50
assert new_x.eval() > 50
```

## Next Steps


---

*Source: test_pytensorf.py:681 | Complexity: Intermediate | Last updated: 2026-05-18*