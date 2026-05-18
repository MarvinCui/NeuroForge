# How To: F Output

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test f output

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.glm`


## Step-by-Step Guide

### Step 1: Assign res = RESULTS.Fcontrast(...)

```python
res = RESULTS.Fcontrast([1, 0])
```

**Verification:**
```python
assert_array_almost_equal(exp_f, res.F)
```

### Step 2: Assign exp_f = value

```python
exp_f = RESULTS.t(0) ** 2
```

**Verification:**
```python
assert_array_almost_equal(exp_f, res.F)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(exp_f, res.F)
```

**Verification:**
```python
assert_array_almost_equal(31.06, res.F, 2)
```

### Step 4: Assign res = RESULTS.Fcontrast(...)

```python
res = RESULTS.Fcontrast(np.array([1, 0]))
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(exp_f, res.F)
```

### Step 6: Assign res = RESULTS.Fcontrast(...)

```python
res = RESULTS.Fcontrast(np.eye(2))
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(31.06, res.F, 2)
```


## Complete Example

```python
# Workflow
res = RESULTS.Fcontrast([1, 0])
exp_f = RESULTS.t(0) ** 2
assert_array_almost_equal(exp_f, res.F)
res = RESULTS.Fcontrast(np.array([1, 0]))
assert_array_almost_equal(exp_f, res.F)
res = RESULTS.Fcontrast(np.eye(2))
assert_array_almost_equal(31.06, res.F, 2)
```

## Next Steps


---

*Source: test_model.py:120 | Complexity: Intermediate | Last updated: 2026-05-18*