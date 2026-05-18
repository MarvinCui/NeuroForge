# How To: Cubic Spline Derivative

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cubic spline derivative

## Prerequisites

**Required Modules:**
- `functools`
- `operator`
- `numpy`
- `numpy.testing`
- `scipy`
- `dipy.align`
- `dipy.align.parzenhist`
- `dipy.align.transforms`
- `dipy.core.interpolation`
- `dipy.core.ndindex`
- `dipy.data`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign in_list = value

```python
in_list = []
```

**Verification:**
```python
assert_array_almost_equal(actual, expected)
```

### Step 2: Assign h = 1e-06

```python
h = 1e-06
```

### Step 3: Assign in_list = np.array(...)

```python
in_list = np.array(in_list)
```

### Step 4: Assign input_h = value

```python
input_h = in_list + h
```

### Step 5: Assign s = np.array(...)

```python
s = np.array(cubic_spline(in_list))
```

### Step 6: Assign s_h = np.array(...)

```python
s_h = np.array(cubic_spline(input_h))
```

### Step 7: Assign expected = value

```python
expected = (s_h - s) / h
```

### Step 8: Assign actual = cubic_spline_derivative(...)

```python
actual = cubic_spline_derivative(in_list)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(actual, expected)
```

### Step 10: Assign x = value

```python
x = t + epsilon
```

### Step 11: Call in_list.append()

```python
in_list.append(x)
```


## Complete Example

```python
# Workflow
in_list = []
for epsilon in [-1e-09, 0.0, 1e-09]:
    for t in [-2.0, -1.0, 0.0, 1.0, 2.0]:
        x = t + epsilon
        in_list.append(x)
h = 1e-06
in_list = np.array(in_list)
input_h = in_list + h
s = np.array(cubic_spline(in_list))
s_h = np.array(cubic_spline(input_h))
expected = (s_h - s) / h
actual = cubic_spline_derivative(in_list)
assert_array_almost_equal(actual, expected)
```

## Next Steps


---

*Source: test_parzenhist.py:105 | Complexity: Advanced | Last updated: 2026-05-18*