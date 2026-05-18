# How To: Commandline Escape

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test CommandLine escape

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `simplejson`
- `logging`
- `pytest`
- `unittest`
- `testing`
- `support`
- `nipype.interfaces.ants`
- `nipype`
- `nipype`
- `nipype.interfaces.fsl`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign test_file = value

```python
test_file = tmp_path / 'test file.txt'
```

**Verification:**
```python
assert result.runtime.stdout == 'content'
```

### Step 2: Call test_file.write_text()

```python
test_file.write_text('content')
```

### Step 3: Assign command = CatCommand(...)

```python
command = CatCommand(in_file=str(test_file))
```

### Step 4: Assign result = command.run(...)

```python
result = command.run()
```

**Verification:**
```python
assert result.runtime.stdout == 'content'
```

### Step 5: Assign in_file = nib.File(...)

```python
in_file = nib.File(desc='a file', exists=True, argstr='%s')
```

### Step 6: Assign input_spec = InputSpec

```python
input_spec = InputSpec
```

### Step 7: Assign _cmd = 'cat'

```python
_cmd = 'cat'
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
test_file = tmp_path / 'test file.txt'
test_file.write_text('content')

class InputSpec(nib.TraitedSpec):
    in_file = nib.File(desc='a file', exists=True, argstr='%s')

class CatCommand(nib.CommandLine):
    input_spec = InputSpec
    _cmd = 'cat'
command = CatCommand(in_file=str(test_file))
result = command.run()
assert result.runtime.stdout == 'content'
```

## Next Steps


---

*Source: test_core.py:613 | Complexity: Intermediate | Last updated: 2026-05-18*