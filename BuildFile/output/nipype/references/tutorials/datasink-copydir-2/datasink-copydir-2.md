# How To: Datasink Copydir 2

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datasink copydir 2

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
# Fixtures: _temp_analyze_files, tmpdir
```

## Step-by-Step Guide

### Step 1: Assign unknown = _temp_analyze_files

```python
orig_img, orig_hdr = _temp_analyze_files
```

**Verification:**
```python
assert not tmpdir.join('basedir', pth.split(sep)[-1], fname).check()
```

### Step 2: Assign unknown = os.path.split(...)

```python
pth, fname = os.path.split(orig_img)
```

**Verification:**
```python
assert tmpdir.join('basedir', 'outdir', pth.split(sep)[-1], fname).check()
```

### Step 3: Assign ds = nio.DataSink(...)

```python
ds = nio.DataSink(base_directory=tmpdir.mkdir('basedir').strpath, parameterization=False)
```

### Step 4: Assign ds.inputs.remove_dest_dir = True

```python
ds.inputs.remove_dest_dir = True
```

### Step 5: Assign ds.inputs.outdir = pth

```python
ds.inputs.outdir = pth
```

### Step 6: Call ds.run()

```python
ds.run()
```

### Step 7: Assign sep = value

```python
sep = os.path.sep
```

**Verification:**
```python
assert not tmpdir.join('basedir', pth.split(sep)[-1], fname).check()
```


## Complete Example

```python
# Setup
# Fixtures: _temp_analyze_files, tmpdir

# Workflow
orig_img, orig_hdr = _temp_analyze_files
pth, fname = os.path.split(orig_img)
ds = nio.DataSink(base_directory=tmpdir.mkdir('basedir').strpath, parameterization=False)
ds.inputs.remove_dest_dir = True
ds.inputs.outdir = pth
ds.run()
sep = os.path.sep
assert not tmpdir.join('basedir', pth.split(sep)[-1], fname).check()
assert tmpdir.join('basedir', 'outdir', pth.split(sep)[-1], fname).check()
```

## Next Steps


---

*Source: test_io.py:513 | Complexity: Intermediate | Last updated: 2026-05-18*