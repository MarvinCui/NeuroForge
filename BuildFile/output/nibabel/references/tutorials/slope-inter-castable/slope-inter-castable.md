# How To: Slope Inter Castable

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test slope inter castable

## Prerequisites

**Required Modules:**
- `itertools`
- `io`
- `platform`
- `numpy`
- `pytest`
- `numpy.testing`
- `arraywriters`
- `casting`
- `testing`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign arr = np.array(...)

```python
arr = np.array([np.inf, np.nan, -np.inf])
```

### Step 2: Assign data = np.array(...)

```python
data = np.array(arr, dtype=in_dtt)
```

### Step 3: Assign in_arr = arr.astype(...)

```python
in_arr = arr.astype(in_dtt)
```

### Step 4: Call SlopeArrayWriter()

```python
SlopeArrayWriter(arr.astype(in_dtt), out_dtt)
```

### Step 5: Call SlopeInterArrayWriter()

```python
SlopeInterArrayWriter(arr.astype(in_dtt), out_dtt)
```

### Step 6: Call SlopeArrayWriter()

```python
SlopeArrayWriter(data, out_dtt)
```

### Step 7: Call SlopeInterArrayWriter()

```python
SlopeInterArrayWriter(data, out_dtt)
```

### Step 8: Call ArrayWriter()

```python
ArrayWriter(data, out_dtt)
```

### Step 9: Assign arr = np.zeros(...)

```python
arr = np.zeros((5,), dtype=in_dtt)
```

### Step 10: Call klass()

```python
klass(arr, out_dtt)
```

### Step 11: Call ArrayWriter()

```python
ArrayWriter(in_arr, out_dtt)
```

### Step 12: Call SlopeArrayWriter()

```python
SlopeArrayWriter(data, out_dtt)
```

### Step 13: Call SlopeInterArrayWriter()

```python
SlopeInterArrayWriter(data, out_dtt)
```

### Step 14: Call ArrayWriter()

```python
ArrayWriter(data, out_dtt)
```


## Complete Example

```python
# Workflow
for in_dtt in FLOAT_TYPES + IUINT_TYPES:
    for out_dtt in NUMERIC_TYPES:
        for klass in (ArrayWriter, SlopeArrayWriter, SlopeInterArrayWriter):
            arr = np.zeros((5,), dtype=in_dtt)
            klass(arr, out_dtt)
arr = np.array([np.inf, np.nan, -np.inf])
for in_dtt in FLOAT_TYPES:
    for out_dtt in IUINT_TYPES:
        in_arr = arr.astype(in_dtt)
        with pytest.raises(WriterError):
            ArrayWriter(in_arr, out_dtt)
        SlopeArrayWriter(arr.astype(in_dtt), out_dtt)
        SlopeInterArrayWriter(arr.astype(in_dtt), out_dtt)
for in_dtt, out_dtt, arr, slope_only, slope_inter, neither in ((np.float32, np.float32, 1, True, True, True), (np.float64, np.float32, 1, True, True, True), (np.float32, np.complex128, 1, True, True, True), (np.uint32, np.complex128, 1, True, True, True), (np.int64, np.float32, 1, True, True, True), (np.float32, np.int16, 1, True, True, False), (np.complex128, np.float32, 1, False, False, False), (np.complex128, np.int16, 1, False, False, False), (np.uint8, np.int16, 1, True, True, True), (np.uint16, np.int16, 1, True, True, True), (np.uint16, np.int16, 2 ** 16 - 1, True, True, False), (np.uint16, np.int16, (0, 2 ** 16 - 1), True, True, False), (np.uint16, np.uint8, 1, True, True, True), (np.int16, np.uint16, 1, True, True, True), (np.int16, np.uint16, -1, True, True, False), (np.int16, np.uint16, (-1, 1), False, True, False), (np.int8, np.uint16, 1, True, True, True), (np.int8, np.uint16, -1, True, True, False), (np.int8, np.uint16, (-1, 1), False, True, False)):
    data = np.array(arr, dtype=in_dtt)
    if slope_only:
        SlopeArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeArrayWriter(data, out_dtt)
    if slope_inter:
        SlopeInterArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            SlopeInterArrayWriter(data, out_dtt)
    if neither:
        ArrayWriter(data, out_dtt)
    else:
        with pytest.raises(WriterError):
            ArrayWriter(data, out_dtt)
```

## Next Steps


---

*Source: test_arraywriters.py:272 | Complexity: Advanced | Last updated: 2026-05-18*