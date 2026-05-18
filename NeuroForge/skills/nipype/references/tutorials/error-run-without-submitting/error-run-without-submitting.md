# How To: Error Run Without Submitting

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test error run without submitting

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `os`
- `pytest`
- `nipype.pipeline`
- `nipype.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, plugin
```

## Step-by-Step Guide

### Step 1: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='rws', base_dir=str(tmp_path))
```

### Step 2: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(SingleNodeTestInterface(), name='n1')
```

### Step 3: Assign n1.inputs.input1 = 1

```python
n1.inputs.input1 = 1
```

### Step 4: Assign n2 = pe.Node(...)

```python
n2 = pe.Node(ErrorInterface(), name='n2', run_without_submitting=True)
```

### Step 5: Assign n3 = pe.Node(...)

```python
n3 = pe.Node(SingleNodeTestInterface(), name='n3')
```

### Step 6: (wf.connect([(n1, n2, [('output1', 'input1')]), (n2, n3, [('output1', 'input1')])]),)

```python
(wf.connect([(n1, n2, [('output1', 'input1')]), (n2, n3, [('output1', 'input1')])]),)
```

### Step 7: Call wf.run()

```python
wf.run(plugin=plugin)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, plugin

# Workflow
wf = pe.Workflow(name='rws', base_dir=str(tmp_path))
n1 = pe.Node(SingleNodeTestInterface(), name='n1')
n1.inputs.input1 = 1
n2 = pe.Node(ErrorInterface(), name='n2', run_without_submitting=True)
n3 = pe.Node(SingleNodeTestInterface(), name='n3')
(wf.connect([(n1, n2, [('output1', 'input1')]), (n2, n3, [('output1', 'input1')])]),)
with pytest.raises(RuntimeError):
    wf.run(plugin=plugin)
```

## Next Steps


---

*Source: test_multiproc.py:168 | Complexity: Intermediate | Last updated: 2026-05-18*