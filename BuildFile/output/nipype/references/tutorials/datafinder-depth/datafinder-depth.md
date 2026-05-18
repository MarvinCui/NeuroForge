# How To: Datafinder Depth

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datafinder depth

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `simplejson`
- `glob`
- `os.path`
- `subprocess`
- `hashlib`
- `collections`
- `pytest`
- `nipype`
- `nipype.interfaces.io`
- `nipype.interfaces.base.traits_extension`
- `nipype.interfaces.base`
- `nipype.utils.filemanip`
- `subprocess`
- `boto`
- `boto.s3.connection`
- `boto3`
- `botocore.utils`
- `paramiko`
- `bids`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign outdir = value

```python
outdir = tmpdir.strpath
```

**Verification:**
```python
assert fname == exp_fname
```

### Step 2: Call os.makedirs()

```python
os.makedirs(os.path.join(outdir, '0', '1', '2', '3'))
```

### Step 3: Assign df = nio.DataFinder(...)

```python
df = nio.DataFinder()
```

### Step 4: Assign df.inputs.root_paths = os.path.join(...)

```python
df.inputs.root_paths = os.path.join(outdir, '0')
```

### Step 5: Assign df.inputs.min_depth = min_depth

```python
df.inputs.min_depth = min_depth
```

### Step 6: Assign df.inputs.max_depth = max_depth

```python
df.inputs.max_depth = max_depth
```

### Step 7: Assign result = df.run(...)

```python
result = df.run()
```

### Step 8: Assign expected = value

```python
expected = [f'{x}' for x in range(min_depth, max_depth + 1)]
```

### Step 9: Assign unknown = os.path.split(...)

```python
_, fname = os.path.split(path)
```

**Verification:**
```python
assert fname == exp_fname
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
outdir = tmpdir.strpath
os.makedirs(os.path.join(outdir, '0', '1', '2', '3'))
df = nio.DataFinder()
df.inputs.root_paths = os.path.join(outdir, '0')
for min_depth in range(4):
    for max_depth in range(min_depth, 4):
        df.inputs.min_depth = min_depth
        df.inputs.max_depth = max_depth
        result = df.run()
        expected = [f'{x}' for x in range(min_depth, max_depth + 1)]
        for path, exp_fname in zip(result.outputs.out_paths, expected):
            _, fname = os.path.split(path)
            assert fname == exp_fname
```

## Next Steps


---

*Source: test_io.py:527 | Complexity: Advanced | Last updated: 2026-05-18*