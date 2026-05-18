# How To: Parse Filename

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test parse filename

## Prerequisites

**Required Modules:**
- `pathlib`
- `pytest`
- `filename_parser`


## Step-by-Step Guide

### Step 1: Assign types_exts = value

```python
types_exts = (('t1', 'ext1'), ('t2', 'ext2'))
```

**Verification:**
```python
assert res == exps
```

### Step 2: Assign exp_in_outs = value

```python
exp_in_outs = ((('/path/fname.funny', ()), ('/path/fname', '.funny', None, None)), (('/path/fnameext2', ()), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2', ('.gz',)), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2.gz', ('.gz',)), ('/path/fname', 'ext2', '.gz', 't2')))
```

**Verification:**
```python
assert res == uexps
```

### Step 3: Assign unknown = inps

```python
pth, sufs = inps
```

**Verification:**
```python
assert res == ('/path/fname', 'ext2', '.GZ', 't2')
```

### Step 4: Assign res = parse_filename(...)

```python
res = parse_filename(pth, types_exts, sufs)
```

**Verification:**
```python
assert res == ('/path/fnameext2', '.GZ', None, None)
```

### Step 5: Assign upth = pth.upper(...)

```python
upth = pth.upper()
```

**Verification:**
```python
assert res == ('/path/fname', 'EXT2', '.gz', 't2')
```

### Step 6: Assign uexps = value

```python
uexps = (exps[0].upper(), exps[1].upper(), exps[2].upper() if exps[2] else None, exps[3])
```

**Verification:**
```python
assert res == ('/path/fnameEXT2', '', '.gz', None)
```

### Step 7: Assign res = parse_filename(...)

```python
res = parse_filename(upth, types_exts, sufs)
```

**Verification:**
```python
assert res == uexps
```

### Step 8: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), False)
```

**Verification:**
```python
assert res == ('/path/fname', 'ext2', '.GZ', 't2')
```

### Step 9: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), True)
```

**Verification:**
```python
assert res == ('/path/fnameext2', '.GZ', None, None)
```

### Step 10: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), False)
```

**Verification:**
```python
assert res == ('/path/fname', 'EXT2', '.gz', 't2')
```

### Step 11: Assign res = parse_filename(...)

```python
res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), True)
```

**Verification:**
```python
assert res == ('/path/fnameEXT2', '', '.gz', None)
```


## Complete Example

```python
# Workflow
types_exts = (('t1', 'ext1'), ('t2', 'ext2'))
exp_in_outs = ((('/path/fname.funny', ()), ('/path/fname', '.funny', None, None)), (('/path/fnameext2', ()), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2', ('.gz',)), ('/path/fname', 'ext2', None, 't2')), (('/path/fnameext2.gz', ('.gz',)), ('/path/fname', 'ext2', '.gz', 't2')))
for inps, exps in exp_in_outs:
    pth, sufs = inps
    res = parse_filename(pth, types_exts, sufs)
    assert res == exps
    upth = pth.upper()
    uexps = (exps[0].upper(), exps[1].upper(), exps[2].upper() if exps[2] else None, exps[3])
    res = parse_filename(upth, types_exts, sufs)
    assert res == uexps
    res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), False)
    assert res == ('/path/fname', 'ext2', '.GZ', 't2')
    res = parse_filename('/path/fnameext2.GZ', types_exts, ('.gz',), True)
    assert res == ('/path/fnameext2', '.GZ', None, None)
    res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), False)
    assert res == ('/path/fname', 'EXT2', '.gz', 't2')
    res = parse_filename('/path/fnameEXT2.gz', types_exts, ('.gz',), True)
    assert res == ('/path/fnameEXT2', '', '.gz', None)
```

## Next Steps


---

*Source: test_filename_parser.py:83 | Complexity: Advanced | Last updated: 2026-05-18*