# How To: Aws Keys From Env

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Function to ensure the DataSink can successfully read in AWS
credentials from the environment variables

## Prerequisites

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


## Step-by-Step Guide

### Step 1: '\n    Function to ensure the DataSink can successfully read in AWS\n    credentials from the environment variables\n    '

```python
'\n    Function to ensure the DataSink can successfully read in AWS\n    credentials from the environment variables\n    '
```

**Verification:**
```python
assert aws_access_key_id == access_key_test
```

### Step 2: Assign ds = nio.DataSink(...)

```python
ds = nio.DataSink()
```

**Verification:**
```python
assert aws_secret_access_key == secret_key_test
```

### Step 3: Assign aws_access_key_id = 'ABCDACCESS'

```python
aws_access_key_id = 'ABCDACCESS'
```

### Step 4: Assign aws_secret_access_key = 'DEFGSECRET'

```python
aws_secret_access_key = 'DEFGSECRET'
```

### Step 5: Assign unknown = aws_access_key_id

```python
os.environ['AWS_ACCESS_KEY_ID'] = aws_access_key_id
```

### Step 6: Assign unknown = aws_secret_access_key

```python
os.environ['AWS_SECRET_ACCESS_KEY'] = aws_secret_access_key
```

### Step 7: Assign unknown = ds._return_aws_keys(...)

```python
access_key_test, secret_key_test = ds._return_aws_keys()
```

**Verification:**
```python
assert aws_access_key_id == access_key_test
```


## Complete Example

```python
# Workflow
'\n    Function to ensure the DataSink can successfully read in AWS\n    credentials from the environment variables\n    '
ds = nio.DataSink()
aws_access_key_id = 'ABCDACCESS'
aws_secret_access_key = 'DEFGSECRET'
os.environ['AWS_ACCESS_KEY_ID'] = aws_access_key_id
os.environ['AWS_SECRET_ACCESS_KEY'] = aws_secret_access_key
access_key_test, secret_key_test = ds._return_aws_keys()
assert aws_access_key_id == access_key_test
assert aws_secret_access_key == secret_key_test
```

## Next Steps


---

*Source: test_io.py:396 | Complexity: Intermediate | Last updated: 2026-05-18*