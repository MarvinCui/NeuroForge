# How To: Generate

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test generate

## Prerequisites

**Required Modules:**
- `nipype2boutiques`
- `nipype.testing`
- `json`


## Step-by-Step Guide

### Step 1: Assign ignored_inputs = value

```python
ignored_inputs = ['args', 'environ', 'output_type']
```

**Verification:**
```python
assert output_desc.get('name') == expected_desc.get('name')
```

### Step 2: Assign desc = generate_boutiques_descriptor(...)

```python
desc = generate_boutiques_descriptor(module='nipype.interfaces.fsl', interface_name='FLIRT', container_image='mcin/docker-fsl:latest', container_index='index.docker.io', container_type='docker', verbose=False, save=False, ignore_inputs=ignored_inputs, author='Oxford Centre for Functional MRI of the Brain (FMRIB)')
```

**Verification:**
```python
assert output_desc.get('author') == expected_desc.get('author')
```

### Step 3: Assign output_desc = json.loads(...)

```python
output_desc = json.loads(desc)
```

**Verification:**
```python
assert output_desc.get('command-line') == expected_desc.get('command-line')
```

### Step 4: Assign expected_desc = json.load(...)

```python
expected_desc = json.load(desc_file)
```

**Verification:**
```python
assert output_desc.get('description') == expected_desc.get('description')
```


## Complete Example

```python
# Workflow
ignored_inputs = ['args', 'environ', 'output_type']
desc = generate_boutiques_descriptor(module='nipype.interfaces.fsl', interface_name='FLIRT', container_image='mcin/docker-fsl:latest', container_index='index.docker.io', container_type='docker', verbose=False, save=False, ignore_inputs=ignored_inputs, author='Oxford Centre for Functional MRI of the Brain (FMRIB)')
with open(example_data('nipype2boutiques_example.json')) as desc_file:
    output_desc = json.loads(desc)
    expected_desc = json.load(desc_file)
    assert output_desc.get('name') == expected_desc.get('name')
    assert output_desc.get('author') == expected_desc.get('author')
    assert output_desc.get('command-line') == expected_desc.get('command-line')
    assert output_desc.get('description') == expected_desc.get('description')
    assert len(output_desc.get('inputs')) == len(expected_desc.get('inputs'))
    assert len(output_desc.get('output-files')) == len(expected_desc.get('output-files'))
    assert output_desc.get('container-image').get('image') == expected_desc.get('container-image').get('image')
```

## Next Steps


---

*Source: test_nipype2boutiques.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*