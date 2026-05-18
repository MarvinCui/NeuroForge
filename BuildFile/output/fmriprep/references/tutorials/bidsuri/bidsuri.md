# How To: Bidsuri

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the BIDSURI interface.

## Prerequisites

**Required Modules:**
- `pytest`
- `fmriprep.interfaces.bids`
- `fmriprep.interfaces.bids`


## Step-by-Step Guide

### Step 1: 'Test the BIDSURI interface.'

```python
'Test the BIDSURI interface.'
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 2: Assign dataset_links = value

```python
dataset_links = {'raw': '/data', 'deriv-0': '/data/derivatives/source-1'}
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 3: Assign out_dir = '/data/derivatives/fmriprep'

```python
out_dir = '/data/derivatives/fmriprep'
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 4: Assign interface = BIDSURI(...)

```python
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 5: Assign interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'

```python
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
```

### Step 6: Assign results = interface.run(...)

```python
results = interface.run()
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 7: Assign interface = BIDSURI(...)

```python
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
```

### Step 8: Assign interface.inputs.in1 = value

```python
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 9: Assign results = interface.run(...)

```python
results = interface.run()
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 10: Assign interface = BIDSURI(...)

```python
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
```

### Step 11: Assign interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'

```python
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
```

### Step 12: Assign interface.inputs.in2 = value

```python
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 13: Assign results = interface.run(...)

```python
results = interface.run()
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 14: Assign interface = BIDSURI(...)

```python
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
```

### Step 15: Assign interface.inputs.in1 = value

```python
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz']
```

### Step 16: Assign interface.inputs.in2 = value

```python
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

### Step 17: Assign results = interface.run(...)

```python
results = interface.run()
```

**Verification:**
```python
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```


## Complete Example

```python
# Workflow
'Test the BIDSURI interface.'
from fmriprep.interfaces.bids import BIDSURI
dataset_links = {'raw': '/data', 'deriv-0': '/data/derivatives/source-1'}
out_dir = '/data/derivatives/fmriprep'
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=1, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = '/data/sub-01/func/sub-01_task-rest_bold.nii.gz'
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
interface = BIDSURI(numinputs=2, dataset_links=dataset_links, out_dir=out_dir)
interface.inputs.in1 = ['/data/sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz']
interface.inputs.in2 = ['/data/derivatives/source-1/sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
results = interface.run()
assert results.outputs.out == ['bids:raw:sub-01/func/sub-01_task-rest_bold.nii.gz', 'bids:raw:sub-01/func/sub-01_task-rest_boldref.nii.gz', 'bids:deriv-0:sub-01/func/sub-01_task-rest_bold.nii.gz', '/out/sub-01/func/sub-01_task-rest_bold.nii.gz']
```

## Next Steps


---

*Source: test_bids.py:6 | Complexity: Advanced | Last updated: 2026-05-18*