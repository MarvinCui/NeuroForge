# How To: Datagrabber Order

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test datagrabber order

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

### Step 1: Assign dg = nio.DataGrabber(...)

```python
dg = nio.DataGrabber(infields=['sid'])
```

**Verification:**
```python
assert 'sub002_L1_R1' in outfiles[0][0]
```

### Step 2: Assign dg.inputs.base_directory = value

```python
dg.inputs.base_directory = tmpdir.strpath
```

**Verification:**
```python
assert 'sub002_L1_R2' in outfiles[0][1]
```

### Step 3: Assign dg.inputs.template = '%s_L%d_R*.q*'

```python
dg.inputs.template = '%s_L%d_R*.q*'
```

**Verification:**
```python
assert 'sub002_L2_R1' in outfiles[1][0]
```

### Step 4: Assign dg.inputs.template_args = value

```python
dg.inputs.template_args = {'outfiles': [['sid', 1], ['sid', 2], ['sid', 3]]}
```

**Verification:**
```python
assert 'sub002_L2_R2' in outfiles[1][1]
```

### Step 5: Assign dg.inputs.sid = 'sub002'

```python
dg.inputs.sid = 'sub002'
```

**Verification:**
```python
assert 'sub002_L3_R2' in outfiles[2][0]
```

### Step 6: Assign dg.inputs.sort_filelist = True

```python
dg.inputs.sort_filelist = True
```

**Verification:**
```python
assert 'sub002_L3_R10' in outfiles[2][1]
```

### Step 7: Assign res = dg.run(...)

```python
res = dg.run()
```

### Step 8: Assign outfiles = value

```python
outfiles = res.outputs.outfiles
```

**Verification:**
```python
assert 'sub002_L1_R1' in outfiles[0][0]
```

### Step 9: Call tmpdir.join.open.close()

```python
tmpdir.join(file_name).open('a').close()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
for file_name in ['sub002_L1_R1.q', 'sub002_L1_R2.q', 'sub002_L2_R1.q', 'sub002_L2_R2.qd', 'sub002_L3_R10.q', 'sub002_L3_R2.q']:
    tmpdir.join(file_name).open('a').close()
dg = nio.DataGrabber(infields=['sid'])
dg.inputs.base_directory = tmpdir.strpath
dg.inputs.template = '%s_L%d_R*.q*'
dg.inputs.template_args = {'outfiles': [['sid', 1], ['sid', 2], ['sid', 3]]}
dg.inputs.sid = 'sub002'
dg.inputs.sort_filelist = True
res = dg.run()
outfiles = res.outputs.outfiles
assert 'sub002_L1_R1' in outfiles[0][0]
assert 'sub002_L1_R2' in outfiles[0][1]
assert 'sub002_L2_R1' in outfiles[1][0]
assert 'sub002_L2_R2' in outfiles[1][1]
assert 'sub002_L3_R2' in outfiles[2][0]
assert 'sub002_L3_R10' in outfiles[2][1]
```

## Next Steps


---

*Source: test_io.py:274 | Complexity: Advanced | Last updated: 2026-05-18*