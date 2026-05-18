# How To: Nlmeans Padding

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nlmeans padding

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `time`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.denoise.denspeed`
- `dipy.denoise.nlmeans`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.omp`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = 100 + 2 * rng.standard_normal((50, 50, 50))
```

**Verification:**
```python
assert_equal(S0.shape, S0n2.shape)
```

### Step 2: Assign S0 = S0.astype(...)

```python
S0 = S0.astype('f8')
```

### Step 3: Assign S0n = add_padding_reflection(...)

```python
S0n = add_padding_reflection(S0, 5)
```

### Step 4: Assign S0n2 = remove_padding(...)

```python
S0n2 = remove_padding(S0n, 5)
```

### Step 5: Call assert_equal()

```python
assert_equal(S0.shape, S0n2.shape)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 100 + 2 * rng.standard_normal((50, 50, 50))
S0 = S0.astype('f8')
S0n = add_padding_reflection(S0, 5)
S0n2 = remove_padding(S0n, 5)
assert_equal(S0.shape, S0n2.shape)
```

## Next Steps


---

*Source: test_nlmeans.py:20 | Complexity: Intermediate | Last updated: 2026-05-18*