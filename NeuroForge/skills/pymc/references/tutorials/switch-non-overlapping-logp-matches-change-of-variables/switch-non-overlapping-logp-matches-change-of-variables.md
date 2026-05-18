# How To: Switch Non Overlapping Logp Matches Change Of Variables

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test switch non overlapping logp matches change of variables

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pymc`
- `pymc.logprob.basic`
- `pymc.logprob.utils`


## Step-by-Step Guide

### Step 1: Assign scale = pt.scalar(...)

```python
scale = pt.scalar('scale')
```

### Step 2: Assign x = pm.Normal.dist(...)

```python
x = pm.Normal.dist(mu=0, sigma=1, size=(3,))
```

### Step 3: Assign y = pt.switch(...)

```python
y = pt.switch(x > 0, x, scale * x)
```

### Step 4: Assign vv = pt.vector(...)

```python
vv = pt.vector('vv')
```

### Step 5: Assign logp_y = logp(...)

```python
logp_y = logp(y, vv)
```

### Step 6: Assign inv = pt.switch(...)

```python
inv = pt.switch(pt.gt(vv, 0), vv, vv / scale)
```

### Step 7: Assign expected = value

```python
expected = logp(x, inv) + pt.switch(pt.gt(vv, 0), 0.0, -pt.log(scale))
```

### Step 8: Assign logp_y_fn = function(...)

```python
logp_y_fn = function([vv, scale], logp_y)
```

### Step 9: Assign expected_fn = function(...)

```python
expected_fn = function([vv, scale], expected)
```

### Step 10: Assign v = np.array(...)

```python
v = np.array([-2.0, 0.0, 1.5])
```

### Step 11: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(logp_y_fn(v, 0.5), expected_fn(v, 0.5))
```

### Step 12: Call logp_y_fn()

```python
logp_y_fn(v, -0.5)
```

### Step 13: Call logp_y_fn()

```python
logp_y_fn(v, 0.0)
```


## Complete Example

```python
# Workflow
scale = pt.scalar('scale')
x = pm.Normal.dist(mu=0, sigma=1, size=(3,))
y = pt.switch(x > 0, x, scale * x)
vv = pt.vector('vv')
logp_y = logp(y, vv)
inv = pt.switch(pt.gt(vv, 0), vv, vv / scale)
expected = logp(x, inv) + pt.switch(pt.gt(vv, 0), 0.0, -pt.log(scale))
logp_y_fn = function([vv, scale], logp_y)
expected_fn = function([vv, scale], expected)
v = np.array([-2.0, 0.0, 1.5])
np.testing.assert_allclose(logp_y_fn(v, 0.5), expected_fn(v, 0.5))
with pytest.raises(ParameterValueError, match='switch non-overlapping scale > 0'):
    logp_y_fn(v, -0.5)
with pytest.raises(ParameterValueError, match='switch non-overlapping scale > 0'):
    logp_y_fn(v, 0.0)
```

## Next Steps


---

*Source: test_switch.py:26 | Complexity: Advanced | Last updated: 2026-05-18*