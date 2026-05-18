# How To: Issue 6335 Dims Containing None

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test issue 6335 dims containing none

## Prerequisites

**Required Modules:**
- `warnings`
- `textwrap`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor.compile.sharedvalue`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.exceptions`
- `pymc.model_graph`


## Step-by-Step Guide

### Step 1: Assign mg = ModelGraph(...)

```python
mg = ModelGraph(pmodel)
```

**Verification:**
```python
assert plates_actual == plates_expected
```

### Step 2: Assign plates_actual = sort_plates(...)

```python
plates_actual = sort_plates(mg.get_plates())
```

### Step 3: Assign plates_expected = sort_plates(...)

```python
plates_expected = sort_plates([Plate(dim_info=DimInfo(names=(None, 'time'), lengths=(3, 5)), variables=[NodeInfo(var=pmodel['n'], node_type=NodeType.DETERMINISTIC)])])
```

**Verification:**
```python
assert plates_actual == plates_expected
```

### Step 4: Assign data = pt.as_tensor(...)

```python
data = pt.as_tensor(np.ones((3, 5)))
```

### Step 5: Call pm.Deterministic()

```python
pm.Deterministic('n', data, dims=(None, 'time'))
```


## Complete Example

```python
# Workflow
with pm.Model(coords={'time': np.arange(5)}) as pmodel:
    data = pt.as_tensor(np.ones((3, 5)))
    pm.Deterministic('n', data, dims=(None, 'time'))
mg = ModelGraph(pmodel)
plates_actual = sort_plates(mg.get_plates())
plates_expected = sort_plates([Plate(dim_info=DimInfo(names=(None, 'time'), lengths=(3, 5)), variables=[NodeInfo(var=pmodel['n'], node_type=NodeType.DETERMINISTIC)])])
assert plates_actual == plates_expected
```

## Next Steps


---

*Source: test_model_graph.py:441 | Complexity: Intermediate | Last updated: 2026-05-18*