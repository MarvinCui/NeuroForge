# How To: Logger Error

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logger error

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `logging`
- `pickle`
- `numpy`
- `py3k`
- `volumeutils`
- `spatialimages`
- `analyze`
- `nifti1`
- `loadsave`
- `casting`
- `numpy.testing`
- `testing`
- `test_wrapstruct`


## Step-by-Step Guide

### Step 1: Assign HC = value

```python
HC = self.header_class
```

**Verification:**
```python
assert_equal(str_io.getvalue(), PIXDIM0_MSG + '\n')
```

### Step 2: Assign hdr = HC(...)

```python
hdr = HC()
```

**Verification:**
```python
assert_raises(HeaderDataError, hdr.copy().check_fix)
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
logger.setLevel(30)
```

### Step 6: Call logger.addHandler()

```python
logger.addHandler(logging.StreamHandler(str_io))
```

### Step 7: Assign unknown = 0

```python
hdr['pixdim'][1] = 0
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

### Step 11: Call assert_equal()

```python
assert_equal(str_io.getvalue(), PIXDIM0_MSG + '\n')
```

### Step 12: Assign imageglobals.error_level = 30

```python
imageglobals.error_level = 30
```

### Step 13: Call assert_raises()

```python
assert_raises(HeaderDataError, hdr.copy().check_fix)
```

### Step 14: Assign unknown = log_cache

```python
imageglobals.logger, imageglobals.error_level = log_cache
```


## Complete Example

```python
# Workflow
HC = self.header_class
hdr = HC()
str_io = StringIO()
logger = logging.getLogger('test.logger')
logger.setLevel(30)
logger.addHandler(logging.StreamHandler(str_io))
hdr['pixdim'][1] = 0
log_cache = (imageglobals.logger, imageglobals.error_level)
try:
    imageglobals.logger = logger
    hdr.copy().check_fix()
    assert_equal(str_io.getvalue(), PIXDIM0_MSG + '\n')
    imageglobals.error_level = 30
    assert_raises(HeaderDataError, hdr.copy().check_fix)
finally:
    imageglobals.logger, imageglobals.error_level = log_cache
```

## Next Steps


---

*Source: test_analyze.py:172 | Complexity: Advanced | Last updated: 2026-05-18*