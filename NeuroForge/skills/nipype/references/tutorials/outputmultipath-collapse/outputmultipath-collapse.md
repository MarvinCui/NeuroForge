# How To: Outputmultipath Collapse

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test an OutputMultiPath whose initial value is ``[[x]]`` to ensure that
it is returned as ``[x]``, regardless of how accessed.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `test_base`
- `test_utils`
- `nipype`
- `nipype`
- `nipype`
- `nipype.interfaces.utility`
- `nipype.pipeline.plugins.base`
- `stat`
- `os`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test an OutputMultiPath whose initial value is ``[[x]]`` to ensure that\n    it is returned as ``[x]``, regardless of how accessed.'

```python
'Test an OutputMultiPath whose initial value is ``[[x]]`` to ensure that\n    it is returned as ``[x]``, regardless of how accessed.'
```

**Verification:**
```python
assert ifres.outputs.out == [4]
```

### Step 2: Assign select_if = niu.Select(...)

```python
select_if = niu.Select(inlist=[[1, 2, 3], [4]], index=1)
```

**Verification:**
```python
assert ndres.outputs.out == [4]
```

### Step 3: Assign select_nd = pe.Node(...)

```python
select_nd = pe.Node(niu.Select(inlist=[[1, 2, 3], [4]], index=1), name='select_nd')
```

**Verification:**
```python
assert select_nd.result.outputs.out == [4]
```

### Step 4: Assign ifres = select_if.run(...)

```python
ifres = select_if.run()
```

### Step 5: Assign ndres = select_nd.run(...)

```python
ndres = select_nd.run()
```

**Verification:**
```python
assert ifres.outputs.out == [4]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test an OutputMultiPath whose initial value is ``[[x]]`` to ensure that\n    it is returned as ``[x]``, regardless of how accessed.'
select_if = niu.Select(inlist=[[1, 2, 3], [4]], index=1)
select_nd = pe.Node(niu.Select(inlist=[[1, 2, 3], [4]], index=1), name='select_nd')
ifres = select_if.run()
ndres = select_nd.run()
assert ifres.outputs.out == [4]
assert ndres.outputs.out == [4]
assert select_nd.result.outputs.out == [4]
```

## Next Steps


---

*Source: test_nodes.py:305 | Complexity: Intermediate | Last updated: 2026-05-18*