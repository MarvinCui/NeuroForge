# How To: Aux Connect Function

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests execution nodes with multiple inputs and auxiliary
function inside the Workflow connect function.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.interfaces`
- `nipype.pipeline.engine`
- `numpy`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'This tests execution nodes with multiple inputs and auxiliary\n    function inside the Workflow connect function.\n    '

```python
'This tests execution nodes with multiple inputs and auxiliary\n    function inside the Workflow connect function.\n    '
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 3: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test_workflow')
```

### Step 4: Assign params = pe.Node(...)

```python
params = pe.Node(utility.IdentityInterface(fields=['size', 'num']), name='params')
```

### Step 5: Assign params.inputs.num = 42

```python
params.inputs.num = 42
```

### Step 6: Assign params.inputs.size = 1

```python
params.inputs.size = 1
```

### Step 7: Assign gen_tuple = pe.Node(...)

```python
gen_tuple = pe.Node(utility.Function(input_names=['size'], output_names=['tuple'], function=_gen_tuple), name='gen_tuple')
```

### Step 8: Assign ssm = pe.Node(...)

```python
ssm = pe.Node(utility.Function(input_names=['a', 'b', 'c'], output_names=['sum', 'sub'], function=_sum_and_sub_mul), name='sum_and_sub_mul')
```

### Step 9: Assign split = pe.Node(...)

```python
split = pe.Node(utility.Split(splits=[1, 1], squeeze=True), name='split')
```

### Step 10: Call wf.connect()

```python
wf.connect([(params, gen_tuple, [(('size', _inc), 'size')]), (params, ssm, [(('num', _inc), 'c')]), (gen_tuple, split, [('tuple', 'inlist')]), (split, ssm, [(('out1', _inc), 'a'), ('out2', 'b')])])
```

### Step 11: Call wf.run()

```python
wf.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'This tests execution nodes with multiple inputs and auxiliary\n    function inside the Workflow connect function.\n    '
tmpdir.chdir()
wf = pe.Workflow(name='test_workflow')

def _gen_tuple(size):
    return [1] * size

def _sum_and_sub_mul(a, b, c):
    return ((a + b) * c, (a - b) * c)

def _inc(x):
    return x + 1
params = pe.Node(utility.IdentityInterface(fields=['size', 'num']), name='params')
params.inputs.num = 42
params.inputs.size = 1
gen_tuple = pe.Node(utility.Function(input_names=['size'], output_names=['tuple'], function=_gen_tuple), name='gen_tuple')
ssm = pe.Node(utility.Function(input_names=['a', 'b', 'c'], output_names=['sum', 'sub'], function=_sum_and_sub_mul), name='sum_and_sub_mul')
split = pe.Node(utility.Split(splits=[1, 1], squeeze=True), name='split')
wf.connect([(params, gen_tuple, [(('size', _inc), 'size')]), (params, ssm, [(('num', _inc), 'c')]), (gen_tuple, split, [('tuple', 'inlist')]), (split, ssm, [(('out1', _inc), 'a'), ('out2', 'b')])])
wf.run()
```

## Next Steps


---

*Source: test_wrappers.py:95 | Complexity: Advanced | Last updated: 2026-05-18*