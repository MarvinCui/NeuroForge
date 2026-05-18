# How To: Datasink To S3

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: This function tests to see if the S3 functionality of a DataSink
works properly

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

### Step 1: '\n    This function tests to see if the S3 functionality of a DataSink\n    works properly\n    '

```python
'\n    This function tests to see if the S3 functionality of a DataSink\n    works properly\n    '
```

**Verification:**
```python
assert src_md5 == dst_md5
```

### Step 2: Assign ds = nio.DataSink(...)

```python
ds = nio.DataSink()
```

### Step 3: Assign bucket_name = 'test'

```python
bucket_name = 'test'
```

### Step 4: Assign container = 'outputs'

```python
container = 'outputs'
```

### Step 5: Assign attr_folder = 'text_file'

```python
attr_folder = 'text_file'
```

### Step 6: Assign output_dir = value

```python
output_dir = 's3://' + bucket_name
```

### Step 7: Assign fakes3_dir = value

```python
fakes3_dir = tmpdir.strpath
```

### Step 8: Assign input_path = dummy_input

```python
input_path = dummy_input
```

### Step 9: Assign proc = Popen(...)

```python
proc = Popen(['fakes3', '-r', fakes3_dir, '-p', '4567'], stdout=open(os.devnull, 'wb'))
```

### Step 10: Assign resource = boto3.resource(...)

```python
resource = boto3.resource(aws_access_key_id='mykey', aws_secret_access_key='mysecret', service_name='s3', endpoint_url='http://127.0.0.1:4567', use_ssl=False)
```

### Step 11: Call resource.meta.client.meta.events.unregister()

```python
resource.meta.client.meta.events.unregister('before-sign.s3', fix_s3_host)
```

### Step 12: Assign bucket = resource.create_bucket(...)

```python
bucket = resource.create_bucket(Bucket=bucket_name)
```

### Step 13: Assign ds.inputs.base_directory = output_dir

```python
ds.inputs.base_directory = output_dir
```

### Step 14: Assign ds.inputs.container = container

```python
ds.inputs.container = container
```

### Step 15: Assign ds.inputs.bucket = bucket

```python
ds.inputs.bucket = bucket
```

### Step 16: Call setattr()

```python
setattr(ds.inputs, attr_folder, input_path)
```

### Step 17: Call ds.run()

```python
ds.run()
```

### Step 18: Assign key = unknown.join(...)

```python
key = '/'.join([container, attr_folder, os.path.basename(input_path)])
```

### Step 19: Assign obj = bucket.Object(...)

```python
obj = bucket.Object(key=key)
```

### Step 20: Assign dst_md5 = obj.e_tag.replace(...)

```python
dst_md5 = obj.e_tag.replace('"', '')
```

### Step 21: Assign src_md5 = hashlib.md5.hexdigest(...)

```python
src_md5 = hashlib.md5(open(input_path, 'rb').read()).hexdigest()
```

### Step 22: Call proc.kill()

```python
proc.kill()
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
'\n    This function tests to see if the S3 functionality of a DataSink\n    works properly\n    '
ds = nio.DataSink()
bucket_name = 'test'
container = 'outputs'
attr_folder = 'text_file'
output_dir = 's3://' + bucket_name
fakes3_dir = tmpdir.strpath
input_path = dummy_input
proc = Popen(['fakes3', '-r', fakes3_dir, '-p', '4567'], stdout=open(os.devnull, 'wb'))
resource = boto3.resource(aws_access_key_id='mykey', aws_secret_access_key='mysecret', service_name='s3', endpoint_url='http://127.0.0.1:4567', use_ssl=False)
resource.meta.client.meta.events.unregister('before-sign.s3', fix_s3_host)
bucket = resource.create_bucket(Bucket=bucket_name)
ds.inputs.base_directory = output_dir
ds.inputs.container = container
ds.inputs.bucket = bucket
setattr(ds.inputs, attr_folder, input_path)
ds.run()
key = '/'.join([container, attr_folder, os.path.basename(input_path)])
obj = bucket.Object(key=key)
dst_md5 = obj.e_tag.replace('"', '')
src_md5 = hashlib.md5(open(input_path, 'rb').read()).hexdigest()
proc.kill()
assert src_md5 == dst_md5
```

## Next Steps


---

*Source: test_io.py:337 | Complexity: Advanced | Last updated: 2026-05-18*