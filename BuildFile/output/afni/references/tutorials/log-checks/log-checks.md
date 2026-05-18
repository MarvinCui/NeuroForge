# How To: Log Checks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test log checks

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

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert_equal(fhdr['an_integer'], 1)
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert_equal(message, 'an_integer should be 1; set an_integer to 1')
```

### Step 3: Assign unknown = 2

```python
hdr['an_integer'] = 2
```

**Verification:**
```python
assert_raises(*raiser)
```

### Step 4: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 40)
```

**Verification:**
```python
assert_equal(message, 'a_str should be lower case; set a_str to lower case')
```

### Step 5: Call assert_equal()

```python
assert_equal(fhdr['an_integer'], 1)
```

**Verification:**
```python
assert_raises(*raiser)
```

### Step 6: Call assert_equal()

```python
assert_equal(message, 'an_integer should be 1; set an_integer to 1')
```

### Step 7: Call assert_raises()

```python
assert_raises(*raiser)
```

### Step 8: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 9: Assign unknown = 'Hello'

```python
hdr['a_str'] = 'Hello'
```

### Step 10: Assign unknown = self.log_chk(...)

```python
fhdr, message, raiser = self.log_chk(hdr, 20)
```

### Step 11: Call assert_equal()

```python
assert_equal(message, 'a_str should be lower case; set a_str to lower case')
```

### Step 12: Call assert_raises()

```python
assert_raises(*raiser)
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
hdr['an_integer'] = 2
fhdr, message, raiser = self.log_chk(hdr, 40)
assert_equal(fhdr['an_integer'], 1)
assert_equal(message, 'an_integer should be 1; set an_integer to 1')
assert_raises(*raiser)
hdr = HC()
hdr['a_str'] = 'Hello'
fhdr, message, raiser = self.log_chk(hdr, 20)
assert_equal(message, 'a_str should be lower case; set a_str to lower case')
assert_raises(*raiser)
```

## Next Steps


---

*Source: test_wrapstruct.py:381 | Complexity: Advanced | Last updated: 2026-05-18*