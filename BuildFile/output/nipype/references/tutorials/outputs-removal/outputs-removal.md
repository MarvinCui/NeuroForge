# How To: Outputs Removal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test outputs removal

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

### Step 1: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(niu.Function(input_names=['arg1'], output_names=['file1', 'file2'], function=test_function), base_dir=tmpdir.strpath, name='testoutputs')
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 2: Assign n1.inputs.arg1 = 1

```python
n1.inputs.arg1 = 1
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 3: Assign n1.config = value

```python
n1.config = {'execution': {'remove_unnecessary_outputs': True}}
```

**Verification:**
```python
assert not tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 4: Assign n1.config = merge_dict(...)

```python
n1.config = merge_dict(deepcopy(config._sections), n1.config)
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file2.txt').check()
```

### Step 5: Call n1.run()

```python
n1.run()
```

**Verification:**
```python
assert tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 6: Assign n1.needed_outputs = value

```python
n1.needed_outputs = ['file2']
```

### Step 7: Call n1.run()

```python
n1.run()
```

**Verification:**
```python
assert not tmpdir.join(n1.name, 'file1.txt').check()
```

### Step 8: Assign file1 = os.path.join(...)

```python
file1 = os.path.join(os.getcwd(), 'file1.txt')
```

### Step 9: Assign file2 = os.path.join(...)

```python
file2 = os.path.join(os.getcwd(), 'file2.txt')
```

### Step 10: Call fp.write()

```python
fp.write('%d' % arg1)
```

### Step 11: Call fp.write()

```python
fp.write('%d' % arg1)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
def test_function(arg1):
    import os
    file1 = os.path.join(os.getcwd(), 'file1.txt')
    file2 = os.path.join(os.getcwd(), 'file2.txt')
    with open(file1, 'w') as fp:
        fp.write('%d' % arg1)
    with open(file2, 'w') as fp:
        fp.write('%d' % arg1)
    return (file1, file2)
n1 = pe.Node(niu.Function(input_names=['arg1'], output_names=['file1', 'file2'], function=test_function), base_dir=tmpdir.strpath, name='testoutputs')
n1.inputs.arg1 = 1
n1.config = {'execution': {'remove_unnecessary_outputs': True}}
n1.config = merge_dict(deepcopy(config._sections), n1.config)
n1.run()
assert tmpdir.join(n1.name, 'file1.txt').check()
assert tmpdir.join(n1.name, 'file1.txt').check()
n1.needed_outputs = ['file2']
n1.run()
assert not tmpdir.join(n1.name, 'file1.txt').check()
assert tmpdir.join(n1.name, 'file2.txt').check()
```

## Next Steps


---

*Source: test_nodes.py:255 | Complexity: Advanced | Last updated: 2026-05-18*