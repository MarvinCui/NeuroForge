# How To: Outputs Removal Wf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test outputs removal wf

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `glob`
- `os`
- `shutil`
- `itertools`
- `pytest`
- `networkx`
- `interfaces`
- `test_base`
- `test_utils`
- `os`
- `os`

**Setup Required:**
```python
# Fixtures: tmpdir, plugin, remove_unnecessary_outputs, keep_inputs
```

## Step-by-Step Guide

### Step 1: Call config.set_default_config()

```python
config.set_default_config()
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file1.txt'))
```

### Step 2: Call config.set()

```python
config.set('execution', 'remove_unnecessary_outputs', remove_unnecessary_outputs)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
```

### Step 3: Call config.set()

```python
config.set('execution', 'keep_inputs', keep_inputs)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt'))
```

### Step 4: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'dir'], function=_test_function), name='n1', base_dir=tmpdir.strpath)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file2.txt')) is not remove_unnecessary_outputs
```

### Step 5: Assign n1.inputs.arg1 = 1

```python
n1.inputs.arg1 = 1
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'subdir', 'file4.txt')) is not remove_unnecessary_outputs
```

### Step 6: Assign n2 = pe.Node(...)

```python
n2 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'n'], function=_test_function2), name='n2', base_dir=tmpdir.strpath)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file3.txt')) is not remove_unnecessary_outputs
```

### Step 7: Assign n2.inputs.arg = 2

```python
n2.inputs.arg = 2
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file3.txt')) is not remove_unnecessary_outputs
```

### Step 8: Assign n3 = pe.Node(...)

```python
n3 = pe.Node(niu.Function(output_names=['n'], function=_test_function3), name='n3', base_dir=tmpdir.strpath)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
```

### Step 9: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='node_rem_test' + plugin, base_dir=tmpdir.strpath)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
```

### Step 10: Call wf.connect()

```python
wf.connect(n1, 'out_file1', n2, 'in_file')
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt')) is not remove_unnecessary_outputs
```

### Step 11: Call wf.run()

```python
wf.run(plugin=plugin)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n4.name, 'file1.txt')) is keep_inputs
```

### Step 12: Assign n4 = pe.Node(...)

```python
n4 = pe.Node(UtilsTestInterface(), name='n4', base_dir=tmpdir.strpath)
```

### Step 13: Call wf.connect()

```python
wf.connect(n2, 'out_file1', n4, 'in_file')
```

### Step 14: Call wf.connect()

```python
wf.connect(n4, ('output1', pick_first), n3, 'arg')
```

### Step 15: Call rmtree()

```python
rmtree(os.path.join(wf.base_dir, wf.name))
```

### Step 16: Call wf.run()

```python
wf.run(plugin=plugin)
```

**Verification:**
```python
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, plugin, remove_unnecessary_outputs, keep_inputs

# Workflow
config.set_default_config()
config.set('execution', 'remove_unnecessary_outputs', remove_unnecessary_outputs)
config.set('execution', 'keep_inputs', keep_inputs)
n1 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'dir'], function=_test_function), name='n1', base_dir=tmpdir.strpath)
n1.inputs.arg1 = 1
n2 = pe.Node(niu.Function(output_names=['out_file1', 'out_file2', 'n'], function=_test_function2), name='n2', base_dir=tmpdir.strpath)
n2.inputs.arg = 2
n3 = pe.Node(niu.Function(output_names=['n'], function=_test_function3), name='n3', base_dir=tmpdir.strpath)
wf = pe.Workflow(name='node_rem_test' + plugin, base_dir=tmpdir.strpath)
wf.connect(n1, 'out_file1', n2, 'in_file')
wf.run(plugin=plugin)
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file2.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'subdir', 'file4.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n1.name, 'file3.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file3.txt')) is not remove_unnecessary_outputs
n4 = pe.Node(UtilsTestInterface(), name='n4', base_dir=tmpdir.strpath)
wf.connect(n2, 'out_file1', n4, 'in_file')

def pick_first(l):
    return l[0]
wf.connect(n4, ('output1', pick_first), n3, 'arg')
rmtree(os.path.join(wf.base_dir, wf.name))
wf.run(plugin=plugin)
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file1.txt'))
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n2.name, 'file2.txt')) is not remove_unnecessary_outputs
assert os.path.exists(os.path.join(wf.base_dir, wf.name, n4.name, 'file1.txt')) is keep_inputs
```

## Next Steps


---

*Source: test_workflows.py:165 | Complexity: Advanced | Last updated: 2026-05-18*