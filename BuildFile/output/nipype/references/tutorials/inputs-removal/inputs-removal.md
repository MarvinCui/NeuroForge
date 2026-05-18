# How To: Inputs Removal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test inputs removal

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

### Step 1: Assign file1 = tmpdir.join(...)

```python
file1 = tmpdir.join('file1.txt')
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 2: Call file1.write()

```python
file1.write('dummy_file')
```

**Verification:**
```python
assert not tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 3: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(UtilsTestInterface(), base_dir=tmpdir.strpath, name='testinputs')
```

### Step 4: Assign n1.inputs.in_file = value

```python
n1.inputs.in_file = file1.strpath
```

### Step 5: Assign n1.config = value

```python
n1.config = {'execution': {'keep_inputs': True}}
```

### Step 6: Assign n1.config = merge_dict(...)

```python
n1.config = merge_dict(deepcopy(config._sections), n1.config)
```

### Step 7: Call n1.run()

```python
n1.run()
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 8: Assign n1.inputs.in_file = value

```python
n1.inputs.in_file = file1.strpath
```

### Step 9: Assign n1.config = value

```python
n1.config = {'execution': {'keep_inputs': False}}
```

### Step 10: Assign n1.config = merge_dict(...)

```python
n1.config = merge_dict(deepcopy(config._sections), n1.config)
```

### Step 11: Assign n1.overwrite = True

```python
n1.overwrite = True
```

### Step 12: Call n1.run()

```python
n1.run()
```

**Verification:**
```python
assert not tmpdir.join(n1.name, 'file1.txt').check()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
file1 = tmpdir.join('file1.txt')
file1.write('dummy_file')
n1 = pe.Node(UtilsTestInterface(), base_dir=tmpdir.strpath, name='testinputs')
n1.inputs.in_file = file1.strpath
n1.config = {'execution': {'keep_inputs': True}}
n1.config = merge_dict(deepcopy(config._sections), n1.config)
n1.run()
assert tmpdir.join(n1.name, 'file1.txt').check()
n1.inputs.in_file = file1.strpath
n1.config = {'execution': {'keep_inputs': False}}
n1.config = merge_dict(deepcopy(config._sections), n1.config)
n1.overwrite = True
n1.run()
assert not tmpdir.join(n1.name, 'file1.txt').check()
```

## Next Steps


---

*Source: test_nodes.py:288 | Complexity: Advanced | Last updated: 2026-05-18*