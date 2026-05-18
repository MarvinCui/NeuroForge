# How To: Cc Factors 2D

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Compares the output of the optimized function to compute the cross-
correlation factors against a direct (not optimized, but less error prone)
implementation.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: '\n    Compares the output of the optimized function to compute the cross-\n    correlation factors against a direct (not optimized, but less error prone)\n    implementation.\n    '

```python
'\n    Compares the output of the optimized function to compute the cross-\n    correlation factors against a direct (not optimized, but less error prone)\n    implementation.\n    '
```

**Verification:**
```python
assert_array_almost_equal(factors, expected)
```

### Step 2: Assign a = np.array.reshape(...)

```python
a = np.array(range(20 * 20), dtype=floating).reshape(20, 20)
```

### Step 3: Assign b = np.array.reshape(...)

```python
b = np.array(range(20 * 20)[::-1], dtype=floating).reshape(20, 20)
```

### Step 4: Assign factors = np.asarray(...)

```python
factors = np.asarray(cc.precompute_cc_factors_2d(a, b, radius))
```

### Step 5: Assign expected = np.asarray(...)

```python
expected = np.asarray(cc.precompute_cc_factors_2d_test(a, b, radius))
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(factors, expected)
```


## Complete Example

```python
# Workflow
'\n    Compares the output of the optimized function to compute the cross-\n    correlation factors against a direct (not optimized, but less error prone)\n    implementation.\n    '
a = np.array(range(20 * 20), dtype=floating).reshape(20, 20)
b = np.array(range(20 * 20)[::-1], dtype=floating).reshape(20, 20)
a /= a.max()
b /= b.max()
for radius in [0, 1, 3, 6]:
    factors = np.asarray(cc.precompute_cc_factors_2d(a, b, radius))
    expected = np.asarray(cc.precompute_cc_factors_2d_test(a, b, radius))
    assert_array_almost_equal(factors, expected)
```

## Next Steps


---

*Source: test_crosscorr.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*