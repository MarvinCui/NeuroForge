# How To: Fail Multiple Clip Single Base

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test failure when multiple clipped_rvs share a single base_rv

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy`
- `scipy.stats`
- `pymc`
- `pymc.logprob`
- `pymc.logprob.transform_value`
- `pymc.logprob.transforms`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: 'Test failure when multiple clipped_rvs share a single base_rv'

```python
'Test failure when multiple clipped_rvs share a single base_rv'
```

### Step 2: Assign base_rv = pt.random.normal(...)

```python
base_rv = pt.random.normal(0, 1)
```

### Step 3: Assign cens_rv1 = pt.clip(...)

```python
cens_rv1 = pt.clip(base_rv, -1, 1)
```

### Step 4: Assign cens_rv1.name = 'cens1'

```python
cens_rv1.name = 'cens1'
```

### Step 5: Assign cens_rv2 = pt.clip(...)

```python
cens_rv2 = pt.clip(base_rv, -1, 1)
```

### Step 6: Assign cens_rv2.name = 'cens2'

```python
cens_rv2.name = 'cens2'
```

### Step 7: Assign cens_vv1 = cens_rv1.clone(...)

```python
cens_vv1 = cens_rv1.clone()
```

### Step 8: Assign cens_vv2 = cens_rv2.clone(...)

```python
cens_vv2 = cens_rv2.clone()
```

### Step 9: Call conditional_logp()

```python
conditional_logp({cens_rv1: cens_vv1, cens_rv2: cens_vv2})
```


## Complete Example

```python
# Workflow
'Test failure when multiple clipped_rvs share a single base_rv'
base_rv = pt.random.normal(0, 1)
cens_rv1 = pt.clip(base_rv, -1, 1)
cens_rv1.name = 'cens1'
cens_rv2 = pt.clip(base_rv, -1, 1)
cens_rv2.name = 'cens2'
cens_vv1 = cens_rv1.clone()
cens_vv2 = cens_rv2.clone()
with pytest.raises(ValueError, match='too many values to unpack'):
    conditional_logp({cens_rv1: cens_vv1, cens_rv2: cens_vv2})
```

## Next Steps


---

*Source: test_censoring.py:186 | Complexity: Advanced | Last updated: 2026-05-18*