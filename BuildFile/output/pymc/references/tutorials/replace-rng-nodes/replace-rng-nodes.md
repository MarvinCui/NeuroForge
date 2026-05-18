# How To: Replace Rng Nodes

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test replace rng nodes

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

### Step 1: Assign rng = pytensor.shared(...)

```python
rng = pytensor.shared(np.random.default_rng())
```

**Verification:**
```python
assert x_rng is cloned_x_rng
```

### Step 2: Assign x = pt.random.normal(...)

```python
x = pt.random.normal(rng=rng)
```

**Verification:**
```python
assert new_x is cloned_x
```

### Step 3: Assign unknown = value

```python
x_rng, *x_non_rng_inputs = x.owner.inputs
```

**Verification:**
```python
assert new_x_rng is not x_rng
```

### Step 4: Assign cloned_x = x.owner.clone.default_output(...)

```python
cloned_x = x.owner.clone().default_output()
```

**Verification:**
```python
assert non_rng_inputs is new_non_rng_inputs
```

### Step 5: Assign unknown = value

```python
cloned_x_rng, *cloned_x_non_rng_inputs = cloned_x.owner.inputs
```

**Verification:**
```python
assert x_rng is cloned_x_rng
```

### Step 6: Assign unknown = replace_rng_nodes(...)

```python
new_x, = replace_rng_nodes([cloned_x])
```

### Step 7: Assign unknown = value

```python
new_x_rng, *new_x_non_rng_inputs = new_x.owner.inputs
```

**Verification:**
```python
assert new_x is cloned_x
```


## Complete Example

```python
# Workflow
rng = pytensor.shared(np.random.default_rng())
x = pt.random.normal(rng=rng)
x_rng, *x_non_rng_inputs = x.owner.inputs
cloned_x = x.owner.clone().default_output()
cloned_x_rng, *cloned_x_non_rng_inputs = cloned_x.owner.inputs
assert x_rng is cloned_x_rng
new_x, = replace_rng_nodes([cloned_x])
new_x_rng, *new_x_non_rng_inputs = new_x.owner.inputs
assert new_x is cloned_x
assert new_x_rng is not x_rng
for non_rng_inputs, new_non_rng_inputs in zip(x_non_rng_inputs, new_x_non_rng_inputs):
    assert non_rng_inputs is new_non_rng_inputs
```

## Next Steps


---

*Source: test_pytensorf.py:599 | Complexity: Intermediate | Last updated: 2026-05-18*