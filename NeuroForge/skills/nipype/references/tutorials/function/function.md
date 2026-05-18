# How To: Function

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test function

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

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign f1 = pe.MapNode(...)

```python
f1 = pe.MapNode(utility.Function(input_names=['size'], output_names=['random_array'], function=gen_random_array), name='random_array', iterfield=['size'])
```

### Step 3: Assign f1.inputs.size = value

```python
f1.inputs.size = [2, 3, 5]
```

### Step 4: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test_workflow')
```

### Step 5: Assign f2 = pe.MapNode(...)

```python
f2 = pe.MapNode(utility.Function(function=increment_array), name='increment_array', iterfield=['in_array'])
```

### Step 6: Call wf.connect()

```python
wf.connect(f1, 'random_array', f2, 'in_array')
```

### Step 7: Assign f3 = pe.Node(...)

```python
f3 = pe.Node(utility.Function(function=concat_sort), name='concat_sort')
```

### Step 8: Call wf.connect()

```python
wf.connect(f2, 'out', f3, 'in_arrays')
```

### Step 9: Call wf.run()

```python
wf.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()

def gen_random_array(size):
    import numpy as np
    return np.random.rand(size, size)
f1 = pe.MapNode(utility.Function(input_names=['size'], output_names=['random_array'], function=gen_random_array), name='random_array', iterfield=['size'])
f1.inputs.size = [2, 3, 5]
wf = pe.Workflow(name='test_workflow')

def increment_array(in_array):
    return in_array + 1
f2 = pe.MapNode(utility.Function(function=increment_array), name='increment_array', iterfield=['in_array'])
wf.connect(f1, 'random_array', f2, 'in_array')
f3 = pe.Node(utility.Function(function=concat_sort), name='concat_sort')
wf.connect(f2, 'out', f3, 'in_arrays')
wf.run()
```

## Next Steps


---

*Source: test_wrappers.py:16 | Complexity: Advanced | Last updated: 2026-05-18*