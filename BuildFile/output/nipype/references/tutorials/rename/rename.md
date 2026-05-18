# How To: Rename

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rename

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `nipype.interfaces`
- `nipype.interfaces.base`
- `nipype.pipeline.engine`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert res.outputs.out_file == outfile
```

### Step 2: Assign _ = open.close(...)

```python
_ = open('file.txt', 'w').close()
```

**Verification:**
```python
assert os.path.exists(outfile)
```

### Step 3: Assign rn = utility.Rename(...)

```python
rn = utility.Rename(in_file='file.txt', format_string='test_file1.txt')
```

**Verification:**
```python
assert hasattr(rn.inputs, 'field1')
```

### Step 4: Assign res = rn.run(...)

```python
res = rn.run()
```

**Verification:**
```python
assert hasattr(rn.inputs, 'field2')
```

### Step 5: Assign outfile = value

```python
outfile = tmpdir.join('test_file1.txt').strpath
```

**Verification:**
```python
assert res.outputs.out_file == outfile
```

### Step 6: Assign rn = utility.Rename(...)

```python
rn = utility.Rename(in_file='file.txt', format_string='%(field1)s_file%(field2)d', keep_ext=True)
```

**Verification:**
```python
assert os.path.exists(outfile)
```

### Step 7: Assign rn.inputs.field1 = 'test'

```python
rn.inputs.field1 = 'test'
```

### Step 8: Assign rn.inputs.field2 = 2

```python
rn.inputs.field2 = 2
```

### Step 9: Assign res = rn.run(...)

```python
res = rn.run()
```

### Step 10: Assign outfile = value

```python
outfile = tmpdir.join('test_file2.txt').strpath
```

**Verification:**
```python
assert res.outputs.out_file == outfile
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
_ = open('file.txt', 'w').close()
rn = utility.Rename(in_file='file.txt', format_string='test_file1.txt')
res = rn.run()
outfile = tmpdir.join('test_file1.txt').strpath
assert res.outputs.out_file == outfile
assert os.path.exists(outfile)
rn = utility.Rename(in_file='file.txt', format_string='%(field1)s_file%(field2)d', keep_ext=True)
assert hasattr(rn.inputs, 'field1')
assert hasattr(rn.inputs, 'field2')
rn.inputs.field1 = 'test'
rn.inputs.field2 = 2
res = rn.run()
outfile = tmpdir.join('test_file2.txt').strpath
assert res.outputs.out_file == outfile
assert os.path.exists(outfile)
```

## Next Steps


---

*Source: test_base.py:11 | Complexity: Advanced | Last updated: 2026-05-18*