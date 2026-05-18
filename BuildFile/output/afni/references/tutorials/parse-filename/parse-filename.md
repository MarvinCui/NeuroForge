# How To: Parse Filename

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test parse filename

## Prerequisites

**Required Modules:**
- `StringIO`
- `filename_parser`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign types_exts = value

```python
types_exts = (('t1', 'ext1'), ('t2', 'ext2'))
```

**Verification:**
```python
assert_equal(res, exps)
```

### Step 2: Assign exp_in_outs = value

```python
exp_in_outs = ((('/path/fname.funny', ()), ('/path/fname', '.funny', None, None)), (('/path/fnameext2', ()), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2', ('.gz',)), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2.gz', ('.gz',)), ('/path/fname', 'ext2', '.gz', 't2')))
```

**Verification:**
```python
assert_equal(res, uexps)
```

### Step 3: Assign unknown = inps

```python
pth, sufs = inps
```

**Verification:**
```python
assert_equal(res, ('/path/fname', 'ext2', '.GZ', 't2'))
```

### Step 4: Assign res = parse_filename(...)

```python
res = parse_filename(pth, types_exts, sufs)
```

**Verification:**
```python
assert_equal(res, ('/path/fnameext2', '.GZ', None, None))
```

### Step 5: Call assert_equal()

```python
assert_equal(res, exps)
```

**Verification:**
```python
assert_equal(res, ('/path/fname', 'EXT2', '.gz', 't2'))
```

### Step 6: Assign upth = pth.upper(...)

```python
upth = pth.upper()
```

**Verification:**
```python
assert_equal(res, ('/path/fnameEXT2', '', '.gz', None))
```

### Step 7: Assign uexps = value

```python
uexps = (exps[0].upper(), exps[1].upper(), exps[2].upper() if exps[2] else None, exps[3])
```

### Step 8: Assign res = parse_filename(...)

```python
res = parse_filename(upth, types_exts, sufs)
```

### Step 9: Call assert_equal()

```python
assert_equal(res, uexps)
```

### Step 10: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), False)
```

### Step 11: Call assert_equal()

```python
assert_equal(res, ('/path/fname', 'ext2', '.GZ', 't2'))
```

### Step 12: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), True)
```

### Step 13: Call assert_equal()

```python
assert_equal(res, ('/path/fnameext2', '.GZ', None, None))
```

### Step 14: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), False)
```

### Step 15: Call assert_equal()

```python
assert_equal(res, ('/path/fname', 'EXT2', '.gz', 't2'))
```

### Step 16: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), True)
```

### Step 17: Call assert_equal()

```python
assert_equal(res, ('/path/fnameEXT2', '', '.gz', None))
```


## Complete Example

```python
# Workflow
types_exts = (('t1', 'ext1'), ('t2', 'ext2'))
exp_in_outs = ((('/path/fname.funny', ()), ('/path/fname', '.funny', None, None)), (('/path/fnameext2', ()), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2', ('.gz',)), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2.gz', ('.gz',)), ('/path/fname', 'ext2', '.gz', 't2')))
for inps, exps in exp_in_outs:
    pth, sufs = inps
    res = parse_filename(pth, types_exts, sufs)
    assert_equal(res, exps)
    upth = pth.upper()
    uexps = (exps[0].upper(), exps[1].upper(), exps[2].upper() if exps[2] else None, exps[3])
    res = parse_filename(upth, types_exts, sufs)
    assert_equal(res, uexps)
    res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), False)
    assert_equal(res, ('/path/fname', 'ext2', '.GZ', 't2'))
    res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), True)
    assert_equal(res, ('/path/fnameext2', '.GZ', None, None))
    res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), False)
    assert_equal(res, ('/path/fname', 'EXT2', '.gz', 't2'))
    res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), True)
    assert_equal(res, ('/path/fnameEXT2', '', '.gz', None))
```

## Next Steps


---

*Source: test_filename_parser.py:111 | Complexity: Advanced | Last updated: 2026-05-18*