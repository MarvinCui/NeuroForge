# How To: Global Commandline Output

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, mock, workflow, integration

## Overview

Workflow: Ensures CommandLine.set_default_terminal_output works

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
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Ensures CommandLine.set_default_terminal_output works'

```python
'Ensures CommandLine.set_default_terminal_output works'
```

**Verification:**
```python
assert ci.terminal_output == 'stream'
```

### Step 2: Assign ci = nib.CommandLine(...)

```python
ci = nib.CommandLine(command='ls -l')
```

**Verification:**
```python
assert ci.terminal_output == 'stream'
```

### Step 3: Assign ci = BET(...)

```python
ci = BET()
```

**Verification:**
```python
assert ci.terminal_output == 'allatonce'
```

### Step 4: Call nib.CommandLine.set_default_terminal_output()

```python
nib.CommandLine.set_default_terminal_output('allatonce')
```

**Verification:**
```python
assert ci.terminal_output == 'file'
```

### Step 5: Assign ci = nib.CommandLine(...)

```python
ci = nib.CommandLine(command='ls -l')
```

**Verification:**
```python
assert ci.terminal_output == 'file'
```

### Step 6: Call nib.CommandLine.set_default_terminal_output()

```python
nib.CommandLine.set_default_terminal_output('file')
```

### Step 7: Assign ci = nib.CommandLine(...)

```python
ci = nib.CommandLine(command='ls -l')
```

**Verification:**
```python
assert ci.terminal_output == 'file'
```

### Step 8: Assign ci = BET(...)

```python
ci = BET()
```

**Verification:**
```python
assert ci.terminal_output == 'file'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Ensures CommandLine.set_default_terminal_output works'
from nipype.interfaces.fsl import BET
ci = nib.CommandLine(command='ls -l')
assert ci.terminal_output == 'stream'
ci = BET()
assert ci.terminal_output == 'stream'
with mock.patch.object(nib.CommandLine, '_terminal_output'):
    nib.CommandLine.set_default_terminal_output('allatonce')
    ci = nib.CommandLine(command='ls -l')
    assert ci.terminal_output == 'allatonce'
    nib.CommandLine.set_default_terminal_output('file')
    ci = nib.CommandLine(command='ls -l')
    assert ci.terminal_output == 'file'
    ci = BET()
    assert ci.terminal_output == 'file'
```

## Next Steps


---

*Source: test_core.py:527 | Complexity: Advanced | Last updated: 2026-05-18*