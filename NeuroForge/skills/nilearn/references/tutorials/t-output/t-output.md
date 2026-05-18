# How To: T Output

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test t output

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm`


## Step-by-Step Guide

### Step 1: Assign exp_t = RESULTS.t(...)

```python
exp_t = RESULTS.t(0)
```

**Verification:**
```python
assert_array_almost_equal(res.t, exp_t)
```

### Step 2: Assign exp_effect = value

```python
exp_effect = RESULTS.theta[0]
```

**Verification:**
```python
assert_array_almost_equal(res.effect, exp_effect)
```

### Step 3: Assign exp_sd = value

```python
exp_sd = exp_effect / exp_t
```

**Verification:**
```python
assert_array_almost_equal(res.sd, exp_sd)
```

### Step 4: Assign res = RESULTS.Tcontrast(...)

```python
res = RESULTS.Tcontrast([1, 0])
```

**Verification:**
```python
assert res.t is None
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.t, exp_t)
```

**Verification:**
```python
assert_array_almost_equal(res.effect, exp_effect)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.effect, exp_effect)
```

**Verification:**
```python
assert res.sd is None
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.sd, exp_sd)
```

**Verification:**
```python
assert_array_almost_equal(res.t, exp_t)
```

### Step 8: Assign res = RESULTS.Tcontrast(...)

```python
res = RESULTS.Tcontrast([1, 0], store=('effect',))
```

**Verification:**
```python
assert res.effect is None
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.effect, exp_effect)
```

**Verification:**
```python
assert res.sd is None
```

### Step 10: Assign res = RESULTS.Tcontrast(...)

```python
res = RESULTS.Tcontrast([1, 0], store=('t',))
```

**Verification:**
```python
assert res.t is None
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.t, exp_t)
```

**Verification:**
```python
assert res.effect is None
```

### Step 12: Assign res = RESULTS.Tcontrast(...)

```python
res = RESULTS.Tcontrast([1, 0], store=('sd',))
```

**Verification:**
```python
assert_array_almost_equal(res.sd, exp_sd)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.sd, exp_sd)
```

**Verification:**
```python
assert res.t is None
```

### Step 14: Assign res = RESULTS.Tcontrast(...)

```python
res = RESULTS.Tcontrast([1, 0], store=('effect', 'sd'))
```

**Verification:**
```python
assert_array_almost_equal(res.effect, exp_effect)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.effect, exp_effect)
```

**Verification:**
```python
assert_array_almost_equal(res.sd, exp_sd)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(res.sd, exp_sd)
```


## Complete Example

```python
# Workflow
exp_t = RESULTS.t(0)
exp_effect = RESULTS.theta[0]
exp_sd = exp_effect / exp_t
res = RESULTS.Tcontrast([1, 0])
assert_array_almost_equal(res.t, exp_t)
assert_array_almost_equal(res.effect, exp_effect)
assert_array_almost_equal(res.sd, exp_sd)
res = RESULTS.Tcontrast([1, 0], store=('effect',))
assert res.t is None
assert_array_almost_equal(res.effect, exp_effect)
assert res.sd is None
res = RESULTS.Tcontrast([1, 0], store=('t',))
assert_array_almost_equal(res.t, exp_t)
assert res.effect is None
assert res.sd is None
res = RESULTS.Tcontrast([1, 0], store=('sd',))
assert res.t is None
assert res.effect is None
assert_array_almost_equal(res.sd, exp_sd)
res = RESULTS.Tcontrast([1, 0], store=('effect', 'sd'))
assert res.t is None
assert_array_almost_equal(res.effect, exp_effect)
assert_array_almost_equal(res.sd, exp_sd)
```

## Next Steps


---

*Source: test_model.py:83 | Complexity: Advanced | Last updated: 2026-05-18*