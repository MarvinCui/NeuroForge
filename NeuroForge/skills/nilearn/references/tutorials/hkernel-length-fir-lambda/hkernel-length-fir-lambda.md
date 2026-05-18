# How To: Hkernel Length Fir Lambda

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the hrf computation.

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm.first_level.hemodynamic_models`


## Step-by-Step Guide

### Step 1: 'Test the hrf computation.'

```python
'Test the hrf computation.'
```

**Verification:**
```python
assert len(h) == 4
```

### Step 2: Assign t_r = 2.0

```python
t_r = 2.0
```

**Verification:**
```python
assert len(h) == 1
```

### Step 3: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel('fir', t_r, fir_delays=np.arange(4))
```

**Verification:**
```python
assert len(h) == 1
```

### Step 4: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel(lambda t_r, ov: np.ones(int(t_r * ov)), t_r)
```

**Verification:**
```python
assert len(h) == 1
```

### Step 5: Assign h = _hrf_kernel(...)

```python
h = _hrf_kernel([lambda t_r, ov: np.ones(int(t_r * ov))], t_r)
```

**Verification:**
```python
assert len(h) == 1
```


## Complete Example

```python
# Workflow
'Test the hrf computation.'
t_r = 2.0
h = _hrf_kernel('fir', t_r, fir_delays=np.arange(4))
assert len(h) == 4
h = _hrf_kernel(lambda t_r, ov: np.ones(int(t_r * ov)), t_r)
assert len(h) == 1
h = _hrf_kernel([lambda t_r, ov: np.ones(int(t_r * ov))], t_r)
assert len(h) == 1
```

## Next Steps


---

*Source: test_hemodynamic_models.py:292 | Complexity: Intermediate | Last updated: 2026-05-18*