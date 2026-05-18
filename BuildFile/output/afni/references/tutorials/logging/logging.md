# How To: Logging

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logging

## Prerequisites

**Required Modules:**
- `py3k`
- `logging`
- `batteryrunners`
- `testing`


## Step-by-Step Guide

### Step 1: Assign rep = Report(...)

```python
rep = Report(ValueError, 20, 'msg', 'fix')
```

**Verification:**
```python
assert_equal(str_io.getvalue(), '')
```

### Step 2: Assign str_io = StringIO(...)

```python
str_io = StringIO()
```

**Verification:**
```python
assert_equal(str_io.getvalue(), 'msg; fix\n')
```

### Step 3: Assign logger = logging.getLogger(...)

```python
logger = logging.getLogger('test.logger')
```

### Step 4: Call logger.setLevel()

```python
logger.setLevel(30)
```

### Step 5: Call logger.addHandler()

```python
logger.addHandler(logging.StreamHandler(str_io))
```

### Step 6: Call rep.log_raise()

```python
rep.log_raise(logger)
```

### Step 7: Call assert_equal()

```python
assert_equal(str_io.getvalue(), '')
```

### Step 8: Assign rep.problem_level = 30

```python
rep.problem_level = 30
```

### Step 9: Call rep.log_raise()

```python
rep.log_raise(logger)
```

### Step 10: Call assert_equal()

```python
assert_equal(str_io.getvalue(), 'msg; fix\n')
```

### Step 11: Call str_io.truncate()

```python
str_io.truncate(0)
```

### Step 12: Call str_io.seek()

```python
str_io.seek(0)
```


## Complete Example

```python
# Workflow
rep = Report(ValueError, 20, 'msg', 'fix')
str_io = StringIO()
logger = logging.getLogger('test.logger')
logger.setLevel(30)
logger.addHandler(logging.StreamHandler(str_io))
rep.log_raise(logger)
assert_equal(str_io.getvalue(), '')
rep.problem_level = 30
rep.log_raise(logger)
assert_equal(str_io.getvalue(), 'msg; fix\n')
str_io.truncate(0)
str_io.seek(0)
```

## Next Steps


---

*Source: test_batteryrunners.py:140 | Complexity: Advanced | Last updated: 2026-05-18*