# How To: No More Gpu Threads Than Specified

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test no more gpu threads than specified

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

### Step 4: Assign n1.inputs.use_gpu = True

```python
n1.inputs.use_gpu = True
```

### Step 5: Assign n1.inputs.input1 = 4

```python
n1.inputs.input1 = 4
```

### Step 6: Call pipe.add_nodes()

```python
pipe.add_nodes([n1])
```

### Step 7: Assign max_threads = 2

```python
max_threads = 2
```

### Step 8: Assign max_gpu = 1

```python
max_gpu = 1
```

### Step 9: Call pipe.run()

```python
pipe.run(plugin='MultiProc', plugin_args={'n_procs': max_threads, 'n_gpu_procs': max_gpu})
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
pipe = pe.Workflow(name='pipe')
n1 = pe.Node(SingleNodeTestInterface(), name='n1', n_procs=2)
n1.inputs.use_gpu = True
n1.inputs.input1 = 4
pipe.add_nodes([n1])
max_threads = 2
max_gpu = 1
with pytest.raises(RuntimeError):
    pipe.run(plugin='MultiProc', plugin_args={'n_procs': max_threads, 'n_gpu_procs': max_gpu})
```

## Next Steps


---

*Source: test_multiproc.py:127 | Complexity: Advanced | Last updated: 2026-05-18*