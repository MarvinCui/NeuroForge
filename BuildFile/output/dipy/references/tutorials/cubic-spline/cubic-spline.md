# How To: Cubic Spline

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cubic spline

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
assert_array_almost_equal(actual, np.array(expected, dtype=np.float64))
```

### Step 2: Assign expected = value

```python
expected = []
```

### Step 3: Assign actual = cubic_spline(...)

```python
actual = cubic_spline(np.array(in_list, dtype=np.float64))
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(actual, np.array(expected, dtype=np.float64))
```

### Step 5: Assign x = value

```python
x = t + epsilon
```

### Step 6: Call in_list.append()

```python
in_list.append(x)
```

### Step 7: Assign absx = np.abs(...)

```python
absx = np.abs(x)
```

### Step 8: Assign sqrx = value

```python
sqrx = x * x
```

### Step 9: Call expected.append()

```python
expected.append((4.0 - 6 * sqrx + 3.0 * absx ** 3) / 6.0)
```

### Step 10: Call expected.append()

```python
expected.append((2 - absx) ** 3 / 6.0)
```

### Step 11: Call expected.append()

```python
expected.append(0.0)
```


## Complete Example

```python
# Workflow
in_list = []
expected = []
for epsilon in [-1e-09, 0.0, 1e-09]:
    for t in [-2.0, -1.0, 0.0, 1.0, 2.0]:
        x = t + epsilon
        in_list.append(x)
        absx = np.abs(x)
        sqrx = x * x
        if absx < 1:
            expected.append((4.0 - 6 * sqrx + 3.0 * absx ** 3) / 6.0)
        elif absx < 2:
            expected.append((2 - absx) ** 3 / 6.0)
        else:
            expected.append(0.0)
actual = cubic_spline(np.array(in_list, dtype=np.float64))
assert_array_almost_equal(actual, np.array(expected, dtype=np.float64))
```

## Next Steps


---

*Source: test_parzenhist.py:80 | Complexity: Advanced | Last updated: 2026-05-18*