# How To: Dereferencing

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dereferencing

## Prerequisites

**Required Modules:**
- `json`
- `os`
- `subprocess`
- `collections.abc`
- `pytest`
- `jsonschema.exceptions`
- `bidsschematools`
- `data`
- `re`


## Step-by-Step Guide

### Step 1: Assign orig = value

```python
orig = {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'$ref': 'ReferencedObject', 'Property2': 'value4'}}
```

**Verification:**
```python
assert dereffed == {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'Property1': 'value1', 'Property2': 'value4'}}
```

### Step 2: Assign dereffed = schema.dereference(...)

```python
dereffed = schema.dereference(orig)
```

**Verification:**
```python
assert dereffed == {'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional', 'space': 'optional', 'desc': 'optional'}}}}
```

### Step 3: Assign orig = value

```python
orig = {'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': 'raw.func.entities', 'space': 'optional', 'desc': 'optional'}}}
```

**Verification:**
```python
assert dereffed == {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'space': 'optional', 'desc': 'optional'}}}}
```

### Step 4: Assign sch = types.Namespace.build(...)

```python
sch = types.Namespace.build(orig)
```

**Verification:**
```python
assert dereffed == {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities': {'hemisphere': {'name': 'hemi', 'enum': ['L', 'R']}}}}
```

### Step 5: Assign dereffed = schema.dereference(...)

```python
dereffed = schema.dereference(sch)
```

**Verification:**
```python
assert dereffed == {'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional', 'space': 'optional', 'desc': 'optional'}}}}
```

### Step 6: Assign orig = value

```python
orig = {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': '_DERIV_ENTS'}}}
```

### Step 7: Assign sch = types.Namespace.build(...)

```python
sch = types.Namespace.build(orig)
```

### Step 8: Assign dereffed = schema.dereference(...)

```python
dereffed = schema.dereference(sch)
```

**Verification:**
```python
assert dereffed == {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'space': 'optional', 'desc': 'optional'}}}}
```

### Step 9: Assign orig = value

```python
orig = {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities.hemisphere': {'name': 'hemi', 'enum': [{'$ref': 'objects.enums.left.value'}, {'$ref': 'objects.enums.right.value'}]}}}
```

### Step 10: Assign sch = types.Namespace.build(...)

```python
sch = types.Namespace.build(orig)
```

### Step 11: Assign dereffed = schema.dereference(...)

```python
dereffed = schema.dereference(sch)
```

**Verification:**
```python
assert dereffed == {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities': {'hemisphere': {'name': 'hemi', 'enum': ['L', 'R']}}}}
```


## Complete Example

```python
# Workflow
orig = {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'$ref': 'ReferencedObject', 'Property2': 'value4'}}
dereffed = schema.dereference(orig)
assert dereffed == {'ReferencedObject': {'Property1': 'value1', 'Property2': 'value2'}, 'ReferencingObject': {'Property1': 'value1', 'Property2': 'value4'}}
orig = {'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': 'raw.func.entities', 'space': 'optional', 'desc': 'optional'}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional', 'space': 'optional', 'desc': 'optional'}}}}
orig = {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw.func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}, 'derived.func': {'$ref': 'raw.func', 'entities': {'$ref': '_DERIV_ENTS'}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'_DERIV_ENTS': {'space': 'optional', 'desc': 'optional'}, 'raw': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'subject': 'required', 'session': 'optional', 'task': 'required', 'dir': 'optional'}}}, 'derived': {'func': {'suffix': ['bold', 'cbv'], 'extensions': ['.nii', '.nii.gz'], 'datatype': ['func'], 'entities': {'space': 'optional', 'desc': 'optional'}}}}
orig = {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities.hemisphere': {'name': 'hemi', 'enum': [{'$ref': 'objects.enums.left.value'}, {'$ref': 'objects.enums.right.value'}]}}}
sch = types.Namespace.build(orig)
dereffed = schema.dereference(sch)
assert dereffed == {'objects': {'enums': {'left': {'value': 'L'}, 'right': {'value': 'R'}}, 'entities': {'hemisphere': {'name': 'hemi', 'enum': ['L', 'R']}}}}
```

## Next Steps


---

*Source: test_schema.py:190 | Complexity: Advanced | Last updated: 2026-05-18*