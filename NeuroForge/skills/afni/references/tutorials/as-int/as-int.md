# How To: As Int

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test as int

## Prerequisites

**Required Modules:**
- `numpy`
- `casting`
- `nose`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Call assert_equal()

```python
assert_equal(as_int(2.0), 2)
```

**Verification:**
```python
assert_equal(as_int(2.0), 2)
```

### Step 2: Call assert_equal()

```python
assert_equal(as_int(-2.0), -2)
```

**Verification:**
```python
assert_equal(as_int(-2.0), -2)
```

### Step 3: Call assert_raises()

```python
assert_raises(FloatingError, as_int, 2.1)
```

**Verification:**
```python
assert_raises(FloatingError, as_int, 2.1)
```

### Step 4: Call assert_raises()

```python
assert_raises(FloatingError, as_int, -2.1)
```

**Verification:**
```python
assert_raises(FloatingError, as_int, -2.1)
```

### Step 5: Call assert_equal()

```python
assert_equal(as_int(2.1, False), 2)
```

**Verification:**
```python
assert_equal(as_int(2.1, False), 2)
```

### Step 6: Call assert_equal()

```python
assert_equal(as_int(-2.1, False), -2)
```

**Verification:**
```python
assert_equal(as_int(-2.1, False), -2)
```

### Step 7: Assign v = np.longdouble(...)

```python
v = np.longdouble(2 ** 64)
```

**Verification:**
```python
assert_equal(as_int(v), 2 ** 64)
```

### Step 8: Call assert_equal()

```python
assert_equal(as_int(v), 2 ** 64)
```

**Verification:**
```python
assert_equal(as_int(v), 2 ** (nmant + 1) - 1)
```

### Step 9: Assign v = value

```python
v = np.longdouble(2) ** (nmant + 1) - 1
```

**Verification:**
```python
assert_raises(OverflowError, as_int, val)
```

### Step 10: Call assert_equal()

```python
assert_equal(as_int(v), 2 ** (nmant + 1) - 1)
```

**Verification:**
```python
assert_raises(OverflowError, as_int, -val)
```

### Step 11: Assign nexp64 = floor_log2(...)

```python
nexp64 = floor_log2(type_info(np.float64)['max'])
```

### Step 12: Assign val = value

```python
val = np.longdouble(2 ** nexp64) * 2
```

### Step 13: Call assert_raises()

```python
assert_raises(OverflowError, as_int, val)
```

### Step 14: Call assert_raises()

```python
assert_raises(OverflowError, as_int, -val)
```

### Step 15: Assign nmant = value

```python
nmant = type_info(np.longdouble)['nmant']
```

### Step 16: Assign nmant = 63

```python
nmant = 63
```


## Complete Example

```python
# Workflow
assert_equal(as_int(2.0), 2)
assert_equal(as_int(-2.0), -2)
assert_raises(FloatingError, as_int, 2.1)
assert_raises(FloatingError, as_int, -2.1)
assert_equal(as_int(2.1, False), 2)
assert_equal(as_int(-2.1, False), -2)
v = np.longdouble(2 ** 64)
assert_equal(as_int(v), 2 ** 64)
try:
    nmant = type_info(np.longdouble)['nmant']
except FloatingError:
    nmant = 63
v = np.longdouble(2) ** (nmant + 1) - 1
assert_equal(as_int(v), 2 ** (nmant + 1) - 1)
nexp64 = floor_log2(type_info(np.float64)['max'])
val = np.longdouble(2 ** nexp64) * 2
assert_raises(OverflowError, as_int, val)
assert_raises(OverflowError, as_int, -val)
```

## Next Steps


---

*Source: test_floating.py:101 | Complexity: Advanced | Last updated: 2026-05-18*