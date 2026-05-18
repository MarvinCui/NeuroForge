# How To: Read Write Files

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test read write files

## Prerequisites

**Required Modules:**
- `os`
- `os.path`
- `shutil`
- `tempfile`
- `glob`
- `numpy`
- `py3k`
- `netcdf`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign cwd = os.getcwd(...)

```python
cwd = os.getcwd()
```

### Step 2: Call os.chdir()

```python
os.chdir(cwd)
```

### Step 3: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir)
```

### Step 4: Assign tmpdir = tempfile.mkdtemp(...)

```python
tmpdir = tempfile.mkdtemp()
```

### Step 5: Call os.chdir()

```python
os.chdir(tmpdir)
```

### Step 6: Assign f = make_simple(...)

```python
f = make_simple('simple.nc', 'w')
```

### Step 7: Call f.close()

```python
f.close()
```

### Step 8: Assign f = netcdf_file(...)

```python
f = netcdf_file('simple.nc')
```

### Step 9: yield (assert_true, f.use_mmap)

```python
yield (assert_true, f.use_mmap)
```

### Step 10: Call f.close()

```python
f.close()
```

### Step 11: Assign f = netcdf_file(...)

```python
f = netcdf_file('simple.nc', mmap=False)
```

### Step 12: yield (assert_false, f.use_mmap)

```python
yield (assert_false, f.use_mmap)
```

### Step 13: Call f.close()

```python
f.close()
```

### Step 14: Assign fobj = open(...)

```python
fobj = open('simple.nc', 'rb')
```

### Step 15: Assign f = netcdf_file(...)

```python
f = netcdf_file(fobj)
```

### Step 16: yield (assert_false, f.use_mmap)

```python
yield (assert_false, f.use_mmap)
```

### Step 17: Call f.close()

```python
f.close()
```

### Step 18: yield testargs

```python
yield testargs
```

### Step 19: yield testargs

```python
yield testargs
```

### Step 20: yield testargs

```python
yield testargs
```

### Step 21: Call os.chdir()

```python
os.chdir(cwd)
```

### Step 22: Call shutil.rmtree()

```python
shutil.rmtree(tmpdir)
```


## Complete Example

```python
# Workflow
cwd = os.getcwd()
try:
    tmpdir = tempfile.mkdtemp()
    os.chdir(tmpdir)
    f = make_simple('simple.nc', 'w')
    f.close()
    f = netcdf_file('simple.nc')
    yield (assert_true, f.use_mmap)
    for testargs in gen_for_simple(f):
        yield testargs
    f.close()
    f = netcdf_file('simple.nc', mmap=False)
    yield (assert_false, f.use_mmap)
    for testargs in gen_for_simple(f):
        yield testargs
    f.close()
    fobj = open('simple.nc', 'rb')
    f = netcdf_file(fobj)
    yield (assert_false, f.use_mmap)
    for testargs in gen_for_simple(f):
        yield testargs
    f.close()
except:
    os.chdir(cwd)
    shutil.rmtree(tmpdir)
    raise
os.chdir(cwd)
shutil.rmtree(tmpdir)
```

## Next Steps


---

*Source: test_netcdf.py:42 | Complexity: Advanced | Last updated: 2026-05-18*