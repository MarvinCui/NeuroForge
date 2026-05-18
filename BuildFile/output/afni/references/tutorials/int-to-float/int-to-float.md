# How To: Int To Float

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test int to float

## Prerequisites

**Required Modules:**
- `numpy`
- `casting`
- `nose`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign LD = value

```python
LD = np.longdouble
```

**Verification:**
```python
assert_equal(int_to_float(i, ie3), ie3(i))
```

### Step 2: Assign nmant = value

```python
nmant = type_info(np.float64)['nmant']
```

**Verification:**
```python
assert_equal(int_to_float(-i, ie3), ie3(-i))
```

### Step 3: Assign nexp64 = floor_log2(...)

```python
nexp64 = floor_log2(type_info(np.float64)['max'])
```

**Verification:**
```python
assert_raises(OverflowError, int_to_float, smn, ie3)
```

### Step 4: Assign unknown = value

```python
smn64, smx64 = (-2 ** (nexp64 + 1), 2 ** (nexp64 + 1))
```

**Verification:**
```python
assert_raises(OverflowError, int_to_float, smx, ie3)
```

### Step 5: Call assert_raises()

```python
assert_raises(OverflowError, int_to_float, smn64, LD)
```

**Verification:**
```python
assert_equal(int_to_float(smn, ie3), ie3(smn))
```

### Step 6: Call assert_raises()

```python
assert_raises(OverflowError, int_to_float, smx64, LD)
```

**Verification:**
```python
assert_equal(int_to_float(smx, ie3), ie3(smx))
```

### Step 7: Assign i = value

```python
i = 2 ** (nmant + 1) - 1
```

**Verification:**
```python
assert_equal(int_to_float(i, LD), LD(i))
```

### Step 8: Call assert_equal()

```python
assert_equal(as_int(int_to_float(i, LD)), i)
```

**Verification:**
```python
assert_equal(int_to_float(-i, LD), LD(-i))
```

### Step 9: Call assert_equal()

```python
assert_equal(as_int(int_to_float(-i, LD)), -i)
```

**Verification:**
```python
assert_raises(OverflowError, int_to_float, smn64, LD)
```

### Step 10: Assign nmant = value

```python
nmant = type_info(ie3)['nmant']
```

**Verification:**
```python
assert_raises(OverflowError, int_to_float, smx64, LD)
```

### Step 11: Assign nexp = floor_log2(...)

```python
nexp = floor_log2(type_info(ie3)['max'])
```

**Verification:**
```python
assert_equal(as_int(int_to_float(i, LD)), i)
```

### Step 12: Assign unknown = value

```python
smn, smx = (-2 ** (nexp + 1), 2 ** (nexp + 1))
```

**Verification:**
```python
assert_equal(as_int(int_to_float(-i, LD)), -i)
```

### Step 13: Assign i = value

```python
i = 2 ** p - 1
```

### Step 14: Call assert_equal()

```python
assert_equal(int_to_float(i, LD), LD(i))
```

### Step 15: Call assert_equal()

```python
assert_equal(int_to_float(-i, LD), LD(-i))
```

### Step 16: Assign nmant = value

```python
nmant = type_info(np.longdouble)['nmant']
```

### Step 17: Assign i = value

```python
i = 2 ** p + 1
```

### Step 18: Call assert_equal()

```python
assert_equal(int_to_float(i, ie3), ie3(i))
```

### Step 19: Call assert_equal()

```python
assert_equal(int_to_float(-i, ie3), ie3(-i))
```

### Step 20: Call assert_raises()

```python
assert_raises(OverflowError, int_to_float, smn, ie3)
```

### Step 21: Call assert_raises()

```python
assert_raises(OverflowError, int_to_float, smx, ie3)
```

### Step 22: Call assert_equal()

```python
assert_equal(int_to_float(smn, ie3), ie3(smn))
```

### Step 23: Call assert_equal()

```python
assert_equal(int_to_float(smx, ie3), ie3(smx))
```


## Complete Example

```python
# Workflow
for ie3 in IEEE_floats:
    nmant = type_info(ie3)['nmant']
    for p in range(nmant + 3):
        i = 2 ** p + 1
        assert_equal(int_to_float(i, ie3), ie3(i))
        assert_equal(int_to_float(-i, ie3), ie3(-i))
    nexp = floor_log2(type_info(ie3)['max'])
    smn, smx = (-2 ** (nexp + 1), 2 ** (nexp + 1))
    if ie3 is np.float64:
        assert_raises(OverflowError, int_to_float, smn, ie3)
        assert_raises(OverflowError, int_to_float, smx, ie3)
    else:
        assert_equal(int_to_float(smn, ie3), ie3(smn))
        assert_equal(int_to_float(smx, ie3), ie3(smx))
LD = np.longdouble
nmant = type_info(np.float64)['nmant']
for p in range(nmant + 2):
    i = 2 ** p - 1
    assert_equal(int_to_float(i, LD), LD(i))
    assert_equal(int_to_float(-i, LD), LD(-i))
nexp64 = floor_log2(type_info(np.float64)['max'])
smn64, smx64 = (-2 ** (nexp64 + 1), 2 ** (nexp64 + 1))
assert_raises(OverflowError, int_to_float, smn64, LD)
assert_raises(OverflowError, int_to_float, smx64, LD)
try:
    nmant = type_info(np.longdouble)['nmant']
except FloatingError:
    return
i = 2 ** (nmant + 1) - 1
assert_equal(as_int(int_to_float(i, LD)), i)
assert_equal(as_int(int_to_float(-i, LD)), -i)
```

## Next Steps


---

*Source: test_floating.py:127 | Complexity: Advanced | Last updated: 2026-05-18*