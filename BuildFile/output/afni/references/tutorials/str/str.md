# How To: Str

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test str

## Prerequisites

**Required Modules:**
- `logging`
- `numpy`
- `wrapstruct`
- `batteryrunners`
- `py3k`
- `volumeutils`
- `spatialimages`
- `unittest`
- `numpy.testing`
- `testing`


## Step-by-Step Guide

### Step 1: Assign hdr = self.header_class(...)

```python
hdr = self.header_class()
```

**Verification:**
```python
assert_true(len(s1) > 0)
```

### Step 2: Assign s1 = str(...)

```python
s1 = str(hdr)
```

**Verification:**
```python
assert_true('fullness of heart' not in s1)
```

### Step 3: Call assert_true()

```python
assert_true(len(s1) > 0)
```

**Verification:**
```python
assert_true('fullness of heart' in s2)
```

### Step 4: Call assert_true()

```python
assert_true('fullness of heart' not in s1)
```

### Step 5: Assign rec = Recoder(...)

```python
rec = Recoder([[1, 'fullness of heart']], ('code', 'label'))
```

### Step 6: Assign unknown = rec

```python
hdr._field_recoders['an_integer'] = rec
```

### Step 7: Assign s2 = str(...)

```python
s2 = str(hdr)
```

### Step 8: Call assert_true()

```python
assert_true('fullness of heart' in s2)
```


## Complete Example

```python
# Workflow
hdr = self.header_class()
s1 = str(hdr)
assert_true(len(s1) > 0)
assert_true('fullness of heart' not in s1)
rec = Recoder([[1, 'fullness of heart']], ('code', 'label'))
hdr._field_recoders['an_integer'] = rec
s2 = str(hdr)
assert_true('fullness of heart' in s2)
```

## Next Steps


---

*Source: test_wrapstruct.py:356 | Complexity: Advanced | Last updated: 2026-05-18*