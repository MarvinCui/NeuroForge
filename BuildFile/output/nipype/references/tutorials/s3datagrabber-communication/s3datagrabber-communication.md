# How To: S3Datagrabber Communication

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test s3datagrabber communication

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

### Step 1: Assign dg = nio.S3DataGrabber(...)

```python
dg = nio.S3DataGrabber(infields=['subj_id', 'run_num'], outfields=['func', 'struct'])
```

**Verification:**
```python
assert os.path.join(dg.inputs.local_directory, '/sub001/BOLD/task001_run001/bold.nii.gz') in func_outfiles[0]
```

### Step 2: Assign dg.inputs.anon = True

```python
dg.inputs.anon = True
```

**Verification:**
```python
assert os.path.exists(func_outfiles[0])
```

### Step 3: Assign dg.inputs.bucket = 'openfmri'

```python
dg.inputs.bucket = 'openfmri'
```

**Verification:**
```python
assert os.path.join(dg.inputs.local_directory, '/sub001/anatomy/highres001_brain.nii.gz') in struct_outfiles[0]
```

### Step 4: Assign dg.inputs.bucket_path = 'ds001/'

```python
dg.inputs.bucket_path = 'ds001/'
```

**Verification:**
```python
assert os.path.exists(struct_outfiles[0])
```

### Step 5: Assign dg.inputs.local_directory = value

```python
dg.inputs.local_directory = tmpdir.strpath
```

**Verification:**
```python
assert os.path.join(dg.inputs.local_directory, '/sub002/BOLD/task001_run003/bold.nii.gz') in func_outfiles[1]
```

### Step 6: Assign dg.inputs.sort_filelist = True

```python
dg.inputs.sort_filelist = True
```

**Verification:**
```python
assert os.path.exists(func_outfiles[1])
```

### Step 7: Assign dg.inputs.template = '*'

```python
dg.inputs.template = '*'
```

**Verification:**
```python
assert os.path.join(dg.inputs.local_directory, '/sub002/anatomy/highres001_brain.nii.gz') in struct_outfiles[1]
```

### Step 8: Assign dg.inputs.field_template = dict(...)

```python
dg.inputs.field_template = dict(func='%s/BOLD/task001_%s/bold.nii.gz', struct='%s/anatomy/highres001_brain.nii.gz')
```

**Verification:**
```python
assert os.path.exists(struct_outfiles[1])
```

### Step 9: Assign dg.inputs.subj_id = value

```python
dg.inputs.subj_id = ['sub001', 'sub002']
```

### Step 10: Assign dg.inputs.run_num = value

```python
dg.inputs.run_num = ['run001', 'run003']
```

### Step 11: Assign dg.inputs.template_args = dict(...)

```python
dg.inputs.template_args = dict(func=[['subj_id', 'run_num']], struct=[['subj_id']])
```

### Step 12: Assign res = dg.run(...)

```python
res = dg.run()
```

### Step 13: Assign func_outfiles = value

```python
func_outfiles = res.outputs.func
```

### Step 14: Assign struct_outfiles = value

```python
struct_outfiles = res.outputs.struct
```

**Verification:**
```python
assert os.path.join(dg.inputs.local_directory, '/sub001/BOLD/task001_run001/bold.nii.gz') in func_outfiles[0]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
dg = nio.S3DataGrabber(infields=['subj_id', 'run_num'], outfields=['func', 'struct'])
dg.inputs.anon = True
dg.inputs.bucket = 'openfmri'
dg.inputs.bucket_path = 'ds001/'
dg.inputs.local_directory = tmpdir.strpath
dg.inputs.sort_filelist = True
dg.inputs.template = '*'
dg.inputs.field_template = dict(func='%s/BOLD/task001_%s/bold.nii.gz', struct='%s/anatomy/highres001_brain.nii.gz')
dg.inputs.subj_id = ['sub001', 'sub002']
dg.inputs.run_num = ['run001', 'run003']
dg.inputs.template_args = dict(func=[['subj_id', 'run_num']], struct=[['subj_id']])
res = dg.run()
func_outfiles = res.outputs.func
struct_outfiles = res.outputs.struct
assert os.path.join(dg.inputs.local_directory, '/sub001/BOLD/task001_run001/bold.nii.gz') in func_outfiles[0]
assert os.path.exists(func_outfiles[0])
assert os.path.join(dg.inputs.local_directory, '/sub001/anatomy/highres001_brain.nii.gz') in struct_outfiles[0]
assert os.path.exists(struct_outfiles[0])
assert os.path.join(dg.inputs.local_directory, '/sub002/BOLD/task001_run003/bold.nii.gz') in func_outfiles[1]
assert os.path.exists(func_outfiles[1])
assert os.path.join(dg.inputs.local_directory, '/sub002/anatomy/highres001_brain.nii.gz') in struct_outfiles[1]
assert os.path.exists(struct_outfiles[1])
```

## Next Steps


---

*Source: test_io.py:222 | Complexity: Advanced | Last updated: 2026-05-18*