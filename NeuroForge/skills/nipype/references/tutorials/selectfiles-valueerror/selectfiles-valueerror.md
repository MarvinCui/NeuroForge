# How To: Selectfiles Valueerror

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ValueError when force_lists has field that isn't in template.

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

### Step 1: "Test ValueError when force_lists has field that isn't in template."

```python
"Test ValueError when force_lists has field that isn't in template."
```

### Step 2: Assign base_dir = op.dirname(...)

```python
base_dir = op.dirname(nipype.__file__)
```

### Step 3: Assign templates = value

```python
templates = {'model': 'interfaces/{package}/model.py', 'preprocess': 'interfaces/{package}/pre*.py'}
```

### Step 4: Assign force_lists = value

```python
force_lists = ['model', 'preprocess', 'registration']
```

### Step 5: Assign sf = nio.SelectFiles(...)

```python
sf = nio.SelectFiles(templates, base_directory=base_dir, force_lists=force_lists)
```

### Step 6: Call sf.run()

```python
sf.run()
```


## Complete Example

```python
# Workflow
"Test ValueError when force_lists has field that isn't in template."
base_dir = op.dirname(nipype.__file__)
templates = {'model': 'interfaces/{package}/model.py', 'preprocess': 'interfaces/{package}/pre*.py'}
force_lists = ['model', 'preprocess', 'registration']
sf = nio.SelectFiles(templates, base_directory=base_dir, force_lists=force_lists)
with pytest.raises(ValueError):
    sf.run()
```

## Next Steps


---

*Source: test_io.py:208 | Complexity: Intermediate | Last updated: 2026-05-18*