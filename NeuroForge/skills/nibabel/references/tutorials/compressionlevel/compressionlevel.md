# How To: Compressionlevel

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test compressionlevel

## Prerequisites

**Required Modules:**
- `contextlib`
- `hashlib`
- `os`
- `time`
- `unittest`
- `gzip`
- `io`
- `unittest`
- `pytest`
- `packaging.version`
- `_compression`
- `openers`
- `tmpdirs`
- `indexed_gzip`
- `_compression`


## Step-by-Step Guide

### Step 1: Assign many_selves = value

```python
many_selves = my_self * 50
```

**Verification:**
```python
assert sizes['default'] == sizes[default_val]
```

### Step 2: Assign my_self = fobj.read(...)

```python
my_self = fobj.read()
```

**Verification:**
```python
assert sizes[1] > sizes[5]
```

### Step 3: Assign default_compresslevel = 5

```python
default_compresslevel = 5
```

### Step 4: Assign sizes = value

```python
sizes = {}
```

**Verification:**
```python
assert sizes['default'] == sizes[default_val]
```

### Step 5: Assign fname = value

```python
fname = 'test.' + ext
```

### Step 6: Assign kwargs = value

```python
kwargs = {'mode': 'wb'}
```

### Step 7: Assign unknown = len(...)

```python
sizes[compresslevel] = len(my_selves_smaller)
```

### Step 8: Assign unknown = compresslevel

```python
kwargs['compresslevel'] = compresslevel
```

### Step 9: Call fobj.write()

```python
fobj.write(many_selves)
```

### Step 10: Assign my_selves_smaller = fobj.read(...)

```python
my_selves_smaller = fobj.read()
```


## Complete Example

```python
# Workflow
with open(__file__, 'rb') as fobj:
    my_self = fobj.read()
many_selves = my_self * 50

class MyOpener(Opener):
    default_compresslevel = 5
with InTemporaryDirectory():
    for ext in ('gz', 'bz2', 'GZ', 'gZ', 'BZ2', 'Bz2'):
        for opener, default_val in ((Opener, 1), (MyOpener, 5)):
            sizes = {}
            for compresslevel in ('default', 1, 5):
                fname = 'test.' + ext
                kwargs = {'mode': 'wb'}
                if compresslevel != 'default':
                    kwargs['compresslevel'] = compresslevel
                with opener(fname, **kwargs) as fobj:
                    fobj.write(many_selves)
                with open(fname, 'rb') as fobj:
                    my_selves_smaller = fobj.read()
                sizes[compresslevel] = len(my_selves_smaller)
            assert sizes['default'] == sizes[default_val]
            assert sizes[1] > sizes[5]
```

## Next Steps


---

*Source: test_openers.py:211 | Complexity: Advanced | Last updated: 2026-05-18*