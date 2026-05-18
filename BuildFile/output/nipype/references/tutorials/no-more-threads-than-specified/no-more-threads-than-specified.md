# How To: No More Threads Than Specified

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no more threads than specified

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
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign pipe = pe.Workflow(...)

```python
pipe = pe.Workflow(name='pipe')
```

### Step 3: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(SingleNodeTestInterface(), name='n1', n_procs=2)
```

### Step 4: Assign n2 = pe.Node(...)

```python
n2 = pe.Node(SingleNodeTestInterface(), name='n2', n_procs=2)
```

### Step 5: Assign n3 = pe.Node(...)

```python
n3 = pe.Node(SingleNodeTestInterface(), name='n3', n_procs=4)
```

### Step 6: Assign n4 = pe.Node(...)

```python
n4 = pe.Node(SingleNodeTestInterface(), name='n4', n_procs=2)
```

### Step 7: Call pipe.connect()

```python
pipe.connect(n1, 'output1', n2, 'input1')
```

### Step 8: Call pipe.connect()

```python
pipe.connect(n1, 'output1', n3, 'input1')
```

### Step 9: Call pipe.connect()

```python
pipe.connect(n2, 'output1', n4, 'input1')
```

### Step 10: Call pipe.connect()

```python
pipe.connect(n3, 'output1', n4, 'input2')
```

### Step 11: Assign n1.inputs.input1 = 4

```python
n1.inputs.input1 = 4
```

### Step 12: Assign max_threads = 2

```python
max_threads = 2
```

### Step 13: Call pipe.run()

```python
pipe.run(plugin='MultiProc', plugin_args={'n_procs': max_threads})
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
pipe = pe.Workflow(name='pipe')
n1 = pe.Node(SingleNodeTestInterface(), name='n1', n_procs=2)
n2 = pe.Node(SingleNodeTestInterface(), name='n2', n_procs=2)
n3 = pe.Node(SingleNodeTestInterface(), name='n3', n_procs=4)
n4 = pe.Node(SingleNodeTestInterface(), name='n4', n_procs=2)
pipe.connect(n1, 'output1', n2, 'input1')
pipe.connect(n1, 'output1', n3, 'input1')
pipe.connect(n2, 'output1', n4, 'input1')
pipe.connect(n3, 'output1', n4, 'input2')
n1.inputs.input1 = 4
max_threads = 2
with pytest.raises(RuntimeError):
    pipe.run(plugin='MultiProc', plugin_args={'n_procs': max_threads})
```

## Next Steps


---

*Source: test_multiproc.py:107 | Complexity: Advanced | Last updated: 2026-05-18*