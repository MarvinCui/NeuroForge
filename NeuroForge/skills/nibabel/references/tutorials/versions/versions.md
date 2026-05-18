# How To: Versions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test versions

## Prerequisites

**Required Modules:**
- `builtins`
- `sys`
- `types`
- `unittest`
- `pytest`
- `packaging.version`
- `nibabel.optpkg`
- `nibabel.tripwire`


## Step-by-Step Guide

### Step 1: Assign fake_name = '_a_fake_package'

```python
fake_name = '_a_fake_package'
```

**Verification:**
```python
assert 'fake_pkg' not in sys.modules
```

### Step 2: Assign fake_pkg = types.ModuleType(...)

```python
fake_pkg = types.ModuleType(fake_name)
```

**Verification:**
```python
assert_bad(fake_name)
```

### Step 3: Call assert_bad()

```python
assert_bad(fake_name)
```

**Verification:**
```python
assert_good(fake_name)
```

### Step 4: Assign unknown = fake_pkg

```python
sys.modules[fake_name] = fake_pkg
```

**Verification:**
```python
assert_bad(fake_name, '1.0')
```

### Step 5: Call assert_good()

```python
assert_good(fake_name)
```

**Verification:**
```python
assert_good(fake_name, lambda pkg: True)
```

### Step 6: Call assert_bad()

```python
assert_bad(fake_name, '1.0')
```

**Verification:**
```python
assert_good(fake_name, min_ver)
```

### Step 7: Call assert_good()

```python
assert_good(fake_name, lambda pkg: True)
```

**Verification:**
```python
assert_bad(fake_name, min_ver)
```

### Step 8: Assign fake_pkg.__version__ = '2.0'

```python
fake_pkg.__version__ = '2.0'
```

**Verification:**
```python
assert str(err) == 'These functions need _a_fake_package version >= 3.0'
```

### Step 9: Assign unknown = optional_package(...)

```python
pkg, _, _ = optional_package(fake_name, min_version='3.0')
```

### Step 10: Call assert_good()

```python
assert_good(fake_name, min_ver)
```

### Step 11: Call assert_bad()

```python
assert_bad(fake_name, min_ver)
```

### Step 12: pkg.some_method

```python
pkg.some_method
```

**Verification:**
```python
assert str(err) == 'These functions need _a_fake_package version >= 3.0'
```


## Complete Example

```python
# Workflow
fake_name = '_a_fake_package'
fake_pkg = types.ModuleType(fake_name)
assert 'fake_pkg' not in sys.modules
assert_bad(fake_name)
try:
    sys.modules[fake_name] = fake_pkg
    assert_good(fake_name)
    assert_bad(fake_name, '1.0')
    assert_good(fake_name, lambda pkg: True)
    fake_pkg.__version__ = '2.0'
    for min_ver in (None, '1.0', Version('1.0'), lambda pkg: True):
        assert_good(fake_name, min_ver)
    for min_ver in ('100.0', Version('100.0'), lambda pkg: False):
        assert_bad(fake_name, min_ver)
    pkg, _, _ = optional_package(fake_name, min_version='3.0')
    try:
        pkg.some_method
    except TripWireError as err:
        assert str(err) == 'These functions need _a_fake_package version >= 3.0'
finally:
    del sys.modules[fake_name]
```

## Next Steps


---

*Source: test_optpkg.py:56 | Complexity: Advanced | Last updated: 2026-05-18*