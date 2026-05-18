# How To: Run Multiproc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test run multiproc

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

**Verification:**
```python
assert result == [1, 1]
```

### Step 2: Assign pipe = pe.Workflow(...)

```python
pipe = pe.Workflow(name='pipe')
```

### Step 3: Assign mod1 = pe.Node(...)

```python
mod1 = pe.Node(MultiprocTestInterface(), name='mod1')
```

### Step 4: Assign mod2 = pe.MapNode(...)

```python
mod2 = pe.MapNode(MultiprocTestInterface(), iterfield=['input1'], name='mod2')
```

### Step 5: Call pipe.connect()

```python
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
```

### Step 6: Assign pipe.base_dir = os.getcwd(...)

```python
pipe.base_dir = os.getcwd()
```

### Step 7: Assign mod1.inputs.input1 = 1

```python
mod1.inputs.input1 = 1
```

### Step 8: Assign unknown = 2

```python
pipe.config['execution']['poll_sleep_duration'] = 2
```

### Step 9: Assign execgraph = pipe.run(...)

```python
execgraph = pipe.run(plugin='MultiProc')
```

### Step 10: Assign names = value

```python
names = [node.fullname for node in execgraph.nodes()]
```

### Step 11: Assign node = value

```python
node = list(execgraph.nodes())[names.index('pipe.mod1')]
```

### Step 12: Assign result = node.get_output(...)

```python
result = node.get_output('output1')
```

**Verification:**
```python
assert result == [1, 1]
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
pipe = pe.Workflow(name='pipe')
mod1 = pe.Node(MultiprocTestInterface(), name='mod1')
mod2 = pe.MapNode(MultiprocTestInterface(), iterfield=['input1'], name='mod2')
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
pipe.base_dir = os.getcwd()
mod1.inputs.input1 = 1
pipe.config['execution']['poll_sleep_duration'] = 2
execgraph = pipe.run(plugin='MultiProc')
names = [node.fullname for node in execgraph.nodes()]
node = list(execgraph.nodes())[names.index('pipe.mod1')]
result = node.get_output('output1')
assert result == [1, 1]
```

## Next Steps


---

*Source: test_multiproc.py:40 | Complexity: Advanced | Last updated: 2026-05-18*