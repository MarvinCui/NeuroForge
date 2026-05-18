# How To: Splitext Addext

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test splitext addext

## Prerequisites

**Required Modules:**
- `StringIO`
- `filename_parser`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign res = splitext_addext(...)

```python
res = splitext_addext('fname.ext.gz')
```

**Verification:**
```python
assert_equal(res, ('fname', '.ext', '.gz'))
```

### Step 2: Call assert_equal()

```python
assert_equal(res, ('fname', '.ext', '.gz'))
```

**Verification:**
```python
assert_equal(res, ('fname', '.ext', ''))
```

### Step 3: Assign res = splitext_addext(...)

```python
res = splitext_addext('fname.ext')
```

**Verification:**
```python
assert_equal(res, ('fname', '.ext', '.foo'))
```

### Step 4: Call assert_equal()

```python
assert_equal(res, ('fname', '.ext', ''))
```

**Verification:**
```python
assert_equal(res, ('fname', '.ext', '.FOO'))
```

### Step 5: Assign res = splitext_addext(...)

```python
res = splitext_addext('fname.ext.foo', ('.foo', '.bar'))
```

**Verification:**
```python
assert_equal(res, ('fname.ext', '.FOO', ''))
```

### Step 6: Call assert_equal()

```python
assert_equal(res, ('fname', '.ext', '.foo'))
```

### Step 7: Assign res = splitext_addext(...)

```python
res = splitext_addext('fname.ext.FOO', ('.foo', '.bar'))
```

### Step 8: Call assert_equal()

```python
assert_equal(res, ('fname', '.ext', '.FOO'))
```

### Step 9: Assign res = splitext_addext(...)

```python
res = splitext_addext('fname.ext.FOO', ('.foo', '.bar'), True)
```

### Step 10: Call assert_equal()

```python
assert_equal(res, ('fname.ext', '.FOO', ''))
```


## Complete Example

```python
# Workflow
res = splitext_addext('fname.ext.gz')
assert_equal(res, ('fname', '.ext', '.gz'))
res = splitext_addext('fname.ext')
assert_equal(res, ('fname', '.ext', ''))
res = splitext_addext('fname.ext.foo', ('.foo', '.bar'))
assert_equal(res, ('fname', '.ext', '.foo'))
res = splitext_addext('fname.ext.FOO', ('.foo', '.bar'))
assert_equal(res, ('fname', '.ext', '.FOO'))
res = splitext_addext('fname.ext.FOO', ('.foo', '.bar'), True)
assert_equal(res, ('fname.ext', '.FOO', ''))
```

## Next Steps


---

*Source: test_filename_parser.py:152 | Complexity: Advanced | Last updated: 2026-05-18*