# How To: Debug

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test debug

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `nipype.interfaces.base`
- `pytest`
- `nipype.pipeline.engine`

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
assert exc is None, 'unexpected exception caught'
```

### Step 2: Assign pipe = pe.Workflow(...)

```python
pipe = pe.Workflow(name='pipe')
```

### Step 3: Assign mod1 = pe.Node(...)

```python
mod1 = pe.Node(DebugTestInterface(), name='mod1')
```

### Step 4: Assign mod2 = pe.MapNode(...)

```python
mod2 = pe.MapNode(DebugTestInterface(), iterfield=['input1'], name='mod2')
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

### Step 8: Assign run_wf = value

```python
run_wf = lambda: pipe.run(plugin='Debug')
```

### Step 9: Assign exc = None

```python
exc = None
```

**Verification:**
```python
assert exc is None, 'unexpected exception caught'
```

### Step 10: Call run_wf()

```python
run_wf()
```

### Step 11: Call pipe.run()

```python
pipe.run(plugin='Debug', plugin_args={'callable': callme})
```

### Step 12: Assign exc = e

```python
exc = e
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
pipe = pe.Workflow(name='pipe')
mod1 = pe.Node(DebugTestInterface(), name='mod1')
mod2 = pe.MapNode(DebugTestInterface(), iterfield=['input1'], name='mod2')
pipe.connect([(mod1, mod2, [('output1', 'input1')])])
pipe.base_dir = os.getcwd()
mod1.inputs.input1 = 1
run_wf = lambda: pipe.run(plugin='Debug')
with pytest.raises(ValueError):
    run_wf()
exc = None
try:
    pipe.run(plugin='Debug', plugin_args={'callable': callme})
except Exception as e:
    exc = e
assert exc is None, 'unexpected exception caught'
```

## Next Steps


---

*Source: test_debug.py:35 | Complexity: Advanced | Last updated: 2026-05-18*