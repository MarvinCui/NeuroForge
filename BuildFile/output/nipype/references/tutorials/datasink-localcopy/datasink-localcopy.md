# How To: Datasink Localcopy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Function to validate DataSink will make local copy via local_copy
attribute

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
# Fixtures: dummy_input, tmpdir
```

## Step-by-Step Guide

### Step 1: '\n    Function to validate DataSink will make local copy via local_copy\n    attribute\n    '

```python
'\n    Function to validate DataSink will make local copy via local_copy\n    attribute\n    '
```

**Verification:**
```python
assert src_md5 == dst_md5
```

### Step 2: Assign local_dir = value

```python
local_dir = tmpdir.strpath
```

### Step 3: Assign container = 'outputs'

```python
container = 'outputs'
```

### Step 4: Assign attr_folder = 'text_file'

```python
attr_folder = 'text_file'
```

### Step 5: Assign input_path = dummy_input

```python
input_path = dummy_input
```

### Step 6: Assign ds = nio.DataSink(...)

```python
ds = nio.DataSink()
```

### Step 7: Assign ds.inputs.container = container

```python
ds.inputs.container = container
```

### Step 8: Assign ds.inputs.local_copy = local_dir

```python
ds.inputs.local_copy = local_dir
```

### Step 9: Call setattr()

```python
setattr(ds.inputs, attr_folder, input_path)
```

### Step 10: Assign local_copy = os.path.join(...)

```python
local_copy = os.path.join(local_dir, container, attr_folder, os.path.basename(input_path))
```

### Step 11: Call ds.run()

```python
ds.run()
```

### Step 12: Assign src_md5 = hashlib.md5.hexdigest(...)

```python
src_md5 = hashlib.md5(open(input_path, 'rb').read()).hexdigest()
```

### Step 13: Assign dst_md5 = hashlib.md5.hexdigest(...)

```python
dst_md5 = hashlib.md5(open(local_copy, 'rb').read()).hexdigest()
```

**Verification:**
```python
assert src_md5 == dst_md5
```


## Complete Example

```python
# Setup
# Fixtures: dummy_input, tmpdir

# Workflow
'\n    Function to validate DataSink will make local copy via local_copy\n    attribute\n    '
local_dir = tmpdir.strpath
container = 'outputs'
attr_folder = 'text_file'
input_path = dummy_input
ds = nio.DataSink()
ds.inputs.container = container
ds.inputs.local_copy = local_dir
setattr(ds.inputs, attr_folder, input_path)
local_copy = os.path.join(local_dir, container, attr_folder, os.path.basename(input_path))
ds.run()
src_md5 = hashlib.md5(open(input_path, 'rb').read()).hexdigest()
dst_md5 = hashlib.md5(open(local_copy, 'rb').read()).hexdigest()
assert src_md5 == dst_md5
```

## Next Steps


---

*Source: test_io.py:420 | Complexity: Advanced | Last updated: 2026-05-18*