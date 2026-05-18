# How To: No More Memory Than Specified

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no more memory than specified

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
n1 = pe.Node(SingleNodeTestInterface(), name='n1', mem_gb=1)
```

### Step 4: Assign n2 = pe.Node(...)

```python
n2 = pe.Node(SingleNodeTestInterface(), name='n2', mem_gb=1)
```

### Step 5: Assign n3 = pe.Node(...)

```python
n3 = pe.Node(SingleNodeTestInterface(), name='n3', mem_gb=1)
```

### Step 6: Assign n4 = pe.Node(...)

```python
n4 = pe.Node(SingleNodeTestInterface(), name='n4', mem_gb=1)
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

### Step 11: Assign n1.inputs.input1 = 1

```python
n1.inputs.input1 = 1
```

### Step 12: Assign max_memory = 0.5

```python
max_memory = 0.5
```

### Step 13: Call pipe.run()

```python
pipe.run(plugin='MultiProc', plugin_args={'memory_gb': max_memory, 'n_procs': 2})
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
pipe = pe.Workflow(name='pipe')
n1 = pe.Node(SingleNodeTestInterface(), name='n1', mem_gb=1)
n2 = pe.Node(SingleNodeTestInterface(), name='n2', mem_gb=1)
n3 = pe.Node(SingleNodeTestInterface(), name='n3', mem_gb=1)
n4 = pe.Node(SingleNodeTestInterface(), name='n4', mem_gb=1)
pipe.connect(n1, 'output1', n2, 'input1')
pipe.connect(n1, 'output1', n3, 'input1')
pipe.connect(n2, 'output1', n4, 'input1')
pipe.connect(n3, 'output1', n4, 'input2')
n1.inputs.input1 = 1
max_memory = 0.5
with pytest.raises(RuntimeError):
    pipe.run(plugin='MultiProc', plugin_args={'memory_gb': max_memory, 'n_procs': 2})
```

## Next Steps


---

*Source: test_multiproc.py:86 | Complexity: Advanced | Last updated: 2026-05-18*