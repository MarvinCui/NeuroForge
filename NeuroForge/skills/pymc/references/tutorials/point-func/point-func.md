# How To: Point Func

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test point func

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: capsys
```

## Step-by-Step Guide

### Step 1: Assign unknown = pt.vectors(...)

```python
x, y = pt.vectors('x', 'y')
```

**Verification:**
```python
assert dprint_res == expected_dprint_res
```

### Step 2: Assign outs = value

```python
outs = x * 2 + y ** 2
```

**Verification:**
```python
assert 'shape=(?,)' in captured.out
```

### Step 3: Assign f = compile(...)

```python
f = compile([x, y], outs)
```

### Step 4: Assign point_f = PointFunc(...)

```python
point_f = PointFunc(f)
```

### Step 5: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(point_f({'y': [3], 'x': [2]}), [4 + 9])
```

### Step 6: Assign dprint_res = point_f.dprint(...)

```python
dprint_res = point_f.dprint(file='str')
```

### Step 7: Assign expected_dprint_res = point_f.f.dprint(...)

```python
expected_dprint_res = point_f.f.dprint(file='str')
```

**Verification:**
```python
assert dprint_res == expected_dprint_res
```

### Step 8: Call point_f.dprint()

```python
point_f.dprint(print_shape=True)
```

### Step 9: Assign captured = capsys.readouterr(...)

```python
captured = capsys.readouterr()
```

**Verification:**
```python
assert 'shape=(?,)' in captured.out
```


## Complete Example

```python
# Setup
# Fixtures: capsys

# Workflow
x, y = pt.vectors('x', 'y')
outs = x * 2 + y ** 2
f = compile([x, y], outs)
point_f = PointFunc(f)
np.testing.assert_allclose(point_f({'y': [3], 'x': [2]}), [4 + 9])
dprint_res = point_f.dprint(file='str')
expected_dprint_res = point_f.f.dprint(file='str')
assert dprint_res == expected_dprint_res
point_f.dprint(print_shape=True)
captured = capsys.readouterr()
assert 'shape=(?,)' in captured.out
```

## Next Steps


---

*Source: test_pytensorf.py:762 | Complexity: Advanced | Last updated: 2026-05-18*