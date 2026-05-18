# How To: Pickle Point Func

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Regression test for https://github.com/pymc-devs/pymc/issues/7857

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

### Step 1: '\n    Regression test for https://github.com/pymc-devs/pymc/issues/7857\n    '

```python
'\n    Regression test for https://github.com/pymc-devs/pymc/issues/7857\n    '
```

### Step 2: Assign unknown = pt.vectors(...)

```python
x, y = pt.vectors('x', 'y')
```

### Step 3: Assign outs = value

```python
outs = x * 2 + y ** 2
```

### Step 4: Assign f = compile(...)

```python
f = compile([x, y], outs)
```

### Step 5: Assign point_f = PointFunc(...)

```python
point_f = PointFunc(f)
```

### Step 6: Assign point_f_pickled = cloudpickle.dumps(...)

```python
point_f_pickled = cloudpickle.dumps(point_f)
```

### Step 7: Assign point_f_unpickled = cloudpickle.loads(...)

```python
point_f_unpickled = cloudpickle.loads(point_f_pickled)
```

### Step 8: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(point_f_unpickled({'y': [3], 'x': [2]}), point_f({'y': [3], 'x': [2]}))
```


## Complete Example

```python
# Workflow
'\n    Regression test for https://github.com/pymc-devs/pymc/issues/7857\n    '
import cloudpickle
x, y = pt.vectors('x', 'y')
outs = x * 2 + y ** 2
f = compile([x, y], outs)
point_f = PointFunc(f)
point_f_pickled = cloudpickle.dumps(point_f)
point_f_unpickled = cloudpickle.loads(point_f_pickled)
np.testing.assert_allclose(point_f_unpickled({'y': [3], 'x': [2]}), point_f({'y': [3], 'x': [2]}))
```

## Next Steps


---

*Source: test_pytensorf.py:783 | Complexity: Advanced | Last updated: 2026-05-18*