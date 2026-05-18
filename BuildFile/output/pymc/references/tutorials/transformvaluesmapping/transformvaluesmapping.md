# How To: Transformvaluesmapping

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TransformValuesMapping

## Prerequisites

**Required Modules:**
- `gc`
- `operator`
- `numpy`
- `pytensor`
- `pytest`
- `scipy`
- `numdifftools`
- `pytensor`
- `pytensor`
- `pytensor.compile.builders`
- `pytensor.graph`
- `pytensor.graph.basic`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.logprob`
- `pymc.logprob.abstract`
- `pymc.logprob.transform_value`
- `pymc.logprob.transforms`
- `pymc.testing`
- `tests.logprob.test_transforms`
- `pymc.model.transform.optimization`


## Step-by-Step Guide

### Step 1: Assign x = pt.vector(...)

```python
x = pt.vector()
```

**Verification:**
```python
assert fg._features[-1] is tvm
```

### Step 2: Assign fg = FunctionGraph(...)

```python
fg = FunctionGraph(outputs=[x])
```

### Step 3: Assign tvm = TransformValuesMapping(...)

```python
tvm = TransformValuesMapping({})
```

### Step 4: Call fg.attach_feature()

```python
fg.attach_feature(tvm)
```

### Step 5: Assign tvm2 = TransformValuesMapping(...)

```python
tvm2 = TransformValuesMapping({})
```

### Step 6: Call fg.attach_feature()

```python
fg.attach_feature(tvm2)
```

**Verification:**
```python
assert fg._features[-1] is tvm
```


## Complete Example

```python
# Workflow
x = pt.vector()
fg = FunctionGraph(outputs=[x])
tvm = TransformValuesMapping({})
fg.attach_feature(tvm)
tvm2 = TransformValuesMapping({})
fg.attach_feature(tvm2)
assert fg._features[-1] is tvm
```

## Next Steps


---

*Source: test_transform_value.py:59 | Complexity: Intermediate | Last updated: 2026-05-18*