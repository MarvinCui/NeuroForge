# How To: Local Lift Diracdelta

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test local lift DiracDelta

## Prerequisites

**Required Modules:**
- `pytensor.tensor`
- `pytensor.graph`
- `pytensor.graph.rewriting.basic`
- `pytensor.graph.rewriting.utils`
- `pytensor.tensor.elemwise`
- `pytensor.tensor.subtensor`
- `pymc.distributions.transforms`
- `pymc.logprob.basic`
- `pymc.logprob.rewriting`
- `pymc.logprob.transform_value`
- `pymc.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign c_at = pt.vector(...)

```python
c_at = pt.vector()
```

**Verification:**
```python
assert isinstance(res.owner.op, DiracDelta)
```

### Step 2: Assign dd_at = dirac_delta(...)

```python
dd_at = dirac_delta(c_at)
```

**Verification:**
```python
assert isinstance(res.owner.inputs[0].owner.op, Elemwise)
```

### Step 3: Assign Z_at = pt.cast(...)

```python
Z_at = pt.cast(dd_at, 'int64')
```

**Verification:**
```python
assert isinstance(res.owner.op, DiracDelta)
```

### Step 4: Assign res = rewrite_graph(...)

```python
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
```

**Verification:**
```python
assert isinstance(res.owner.inputs[0].owner.op, DimShuffle)
```

### Step 5: Assign Z_at = dd_at.dimshuffle(...)

```python
Z_at = dd_at.dimshuffle('x', 0)
```

**Verification:**
```python
assert isinstance(res.owner.op, DiracDelta)
```

### Step 6: Assign res = rewrite_graph(...)

```python
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
```

**Verification:**
```python
assert isinstance(res.owner.inputs[0].owner.op, Subtensor)
```

### Step 7: Assign Z_at = value

```python
Z_at = dd_at[0]
```

**Verification:**
```python
assert res is Z_at
```

### Step 8: Assign res = rewrite_graph(...)

```python
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
```

**Verification:**
```python
assert isinstance(res.owner.op, DiracDelta)
```

### Step 9: Assign c_at = pt.matrix(...)

```python
c_at = pt.matrix()
```

### Step 10: Assign dd_at = dirac_delta(...)

```python
dd_at = dirac_delta(c_at)
```

### Step 11: Assign Z_at = value

```python
Z_at = pt.linalg.svd(dd_at)[0]
```

### Step 12: Assign res = rewrite_graph(...)

```python
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
```

**Verification:**
```python
assert res is Z_at
```


## Complete Example

```python
# Workflow
c_at = pt.vector()
dd_at = dirac_delta(c_at)
Z_at = pt.cast(dd_at, 'int64')
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
assert isinstance(res.owner.op, DiracDelta)
assert isinstance(res.owner.inputs[0].owner.op, Elemwise)
Z_at = dd_at.dimshuffle('x', 0)
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
assert isinstance(res.owner.op, DiracDelta)
assert isinstance(res.owner.inputs[0].owner.op, DimShuffle)
Z_at = dd_at[0]
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
assert isinstance(res.owner.op, DiracDelta)
assert isinstance(res.owner.inputs[0].owner.op, Subtensor)
c_at = pt.matrix()
dd_at = dirac_delta(c_at)
Z_at = pt.linalg.svd(dd_at)[0]
res = rewrite_graph(Z_at, custom_rewrite=in2out(local_lift_DiracDelta), clone=False)
assert res is Z_at
```

## Next Steps


---

*Source: test_rewriting.py:54 | Complexity: Advanced | Last updated: 2026-05-18*