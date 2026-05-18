# How To: Logger Error

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test logger error

## Prerequisites

**Required Modules:**
- `logging`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `batteryrunners`
- `casting`
- `spatialimages`
- `volumeutils`
- `wrapstruct`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert str_io.getvalue() == 'a_str should be lower case; set a_str to lower case\n'
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

### Step 3: Assign str_io = StringIO(...)

```python
str_io = StringIO()
```

### Step 4: Assign logger = logging.getLogger(...)

```python
logger = logging.getLogger('test.logger')
```

### Step 5: Call logger.setLevel()

```python
logger.setLevel(20)
```

### Step 6: Call logger.addHandler()

```python
logger.addHandler(logging.StreamHandler(str_io))
```

### Step 7: Assign unknown = 'Fullness'

```python
hdr['a_str'] = 'Fullness'
```

### Step 8: Assign log_cache = value

```python
log_cache = (imageglobals.logger, imageglobals.error_level)
```

### Step 9: Assign imageglobals.logger = logger

```python
imageglobals.logger = logger
```

### Step 10: Call hdr.copy.check_fix()

```python
hdr.copy().check_fix()
```

**Verification:**
```python
assert str_io.getvalue() == 'a_str should be lower case; set a_str to lower case\n'
```

### Step 11: Assign imageglobals.error_level = 20

```python
imageglobals.error_level = 20
```

### Step 12: Assign unknown = log_cache

```python
imageglobals.logger, imageglobals.error_level = log_cache
```

### Step 13: Call hdr.copy.check_fix()

```python
hdr.copy().check_fix()
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
str_io = StringIO()
logger = logging.getLogger('test.logger')
logger.setLevel(20)
logger.addHandler(logging.StreamHandler(str_io))
hdr['a_str'] = 'Fullness'
log_cache = (imageglobals.logger, imageglobals.error_level)
try:
    imageglobals.logger = logger
    hdr.copy().check_fix()
    assert str_io.getvalue() == 'a_str should be lower case; set a_str to lower case\n'
    imageglobals.error_level = 20
    with pytest.raises(HeaderDataError):
        hdr.copy().check_fix()
finally:
    imageglobals.logger, imageglobals.error_level = log_cache
```

## Next Steps


---

*Source: test_wrapstruct.py:475 | Complexity: Advanced | Last updated: 2026-05-18*