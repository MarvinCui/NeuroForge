# How To: Switch Mixture Invalid Bcast

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we don't mark switches where components are broadcasted as measurable

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor`
- `pytensor.compile`
- `pytensor.graph.basic`
- `pytensor.ifelse`
- `pytensor.link.numba`
- `pytensor.tensor.random.basic`
- `pytensor.tensor.shape`
- `pytensor.tensor.subtensor`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pymc.logprob.mixture`
- `pymc.logprob.rewriting`
- `pymc.logprob.utils`
- `pymc.testing`
- `tests.logprob.utils`


## Step-by-Step Guide

### Step 1: "Test that we don't mark switches where components are broadcasted as measurable"

```python
"Test that we don't mark switches where components are broadcasted as measurable"
```

**Verification:**
```python
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

### Step 2: Assign valid_switch_cond = pt.vector(...)

```python
valid_switch_cond = pt.vector('switch_cond', dtype=bool)
```

**Verification:**
```python
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableSwitchMixture)
```

### Step 3: Assign invalid_switch_cond = pt.matrix(...)

```python
invalid_switch_cond = pt.matrix('switch_cond', dtype=bool)
```

**Verification:**
```python
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

### Step 4: Assign valid_true_branch = pt.exp(...)

```python
valid_true_branch = pt.exp(pt.random.normal(size=(4,)))
```

**Verification:**
```python
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

### Step 5: Assign valid_false_branch = pt.abs(...)

```python
valid_false_branch = pt.abs(pt.random.normal(size=(4,)))
```

### Step 6: Assign invalid_false_branch = pt.abs(...)

```python
invalid_false_branch = pt.abs(pt.random.normal(size=()))
```

### Step 7: Assign valid_mix = pt.switch(...)

```python
valid_mix = pt.switch(valid_switch_cond, valid_true_branch, valid_false_branch)
```

### Step 8: Assign fgraph = construct_ir_fgraph(...)

```python
fgraph = construct_ir_fgraph({valid_mix: valid_mix.type()})
```

**Verification:**
```python
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

### Step 9: Assign invalid_mix = pt.switch(...)

```python
invalid_mix = pt.switch(invalid_switch_cond, valid_true_branch, valid_false_branch)
```

### Step 10: Assign fgraph = construct_ir_fgraph(...)

```python
fgraph = construct_ir_fgraph({invalid_mix: invalid_mix.type()})
```

**Verification:**
```python
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

### Step 11: Assign invalid_mix = pt.switch(...)

```python
invalid_mix = pt.switch(valid_switch_cond, valid_true_branch, invalid_false_branch)
```

### Step 12: Assign fgraph = construct_ir_fgraph(...)

```python
fgraph = construct_ir_fgraph({invalid_mix: invalid_mix.type()})
```

**Verification:**
```python
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```


## Complete Example

```python
# Workflow
"Test that we don't mark switches where components are broadcasted as measurable"
valid_switch_cond = pt.vector('switch_cond', dtype=bool)
invalid_switch_cond = pt.matrix('switch_cond', dtype=bool)
valid_true_branch = pt.exp(pt.random.normal(size=(4,)))
valid_false_branch = pt.abs(pt.random.normal(size=(4,)))
invalid_false_branch = pt.abs(pt.random.normal(size=()))
valid_mix = pt.switch(valid_switch_cond, valid_true_branch, valid_false_branch)
fgraph = construct_ir_fgraph({valid_mix: valid_mix.type()})
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
assert isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableSwitchMixture)
invalid_mix = pt.switch(invalid_switch_cond, valid_true_branch, valid_false_branch)
fgraph = construct_ir_fgraph({invalid_mix: invalid_mix.type()})
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
invalid_mix = pt.switch(valid_switch_cond, valid_true_branch, invalid_false_branch)
fgraph = construct_ir_fgraph({invalid_mix: invalid_mix.type()})
assert not isinstance(fgraph.outputs[0].owner.inputs[0].owner.op, MeasurableOp)
```

## Next Steps


---

*Source: test_mixture.py:930 | Complexity: Advanced | Last updated: 2026-05-18*