# How To: Commandline Prefix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test CommandLine prefix

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

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign oop = 'out/of/path'

```python
oop = 'out/of/path'
```

### Step 3: Call os.makedirs()

```python
os.makedirs(oop)
```

### Step 4: Assign script_name = 'test_script.sh'

```python
script_name = 'test_script.sh'
```

### Step 5: Assign script_path = os.path.join(...)

```python
script_path = os.path.join(oop, script_name)
```

### Step 6: Call os.chmod()

```python
os.chmod(script_path, 493)
```

### Step 7: Assign ci = nib.CommandLine(...)

```python
ci = nib.CommandLine(command=script_name)
```

### Step 8: Assign ci = OOPCLI(...)

```python
ci = OOPCLI(command=script_name)
```

### Step 9: Call ci.run()

```python
ci.run()
```

### Step 10: Assign ci = OOPShell(...)

```python
ci = OOPShell(command=script_name)
```

### Step 11: Call ci.run()

```python
ci.run()
```

### Step 12: Assign ci = OOPBadShell(...)

```python
ci = OOPBadShell(command=script_name)
```

### Step 13: Call script_f.write()

```python
script_f.write('#!/usr/bin/env bash\necho Success!')
```

### Step 14: Call ci.run()

```python
ci.run()
```

### Step 15: Assign _cmd_prefix = value

```python
_cmd_prefix = oop + '/'
```

### Step 16: Assign _cmd_prefix = value

```python
_cmd_prefix = f'bash {oop}/'
```

### Step 17: Assign _cmd_prefix = value

```python
_cmd_prefix = f'shell_dne {oop}/'
```

### Step 18: Call ci.run()

```python
ci.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
oop = 'out/of/path'
os.makedirs(oop)
script_name = 'test_script.sh'
script_path = os.path.join(oop, script_name)
with open(script_path, 'w') as script_f:
    script_f.write('#!/usr/bin/env bash\necho Success!')
os.chmod(script_path, 493)
ci = nib.CommandLine(command=script_name)
with pytest.raises(IOError):
    ci.run()

class OOPCLI(nib.CommandLine):
    _cmd_prefix = oop + '/'
ci = OOPCLI(command=script_name)
ci.run()

class OOPShell(nib.CommandLine):
    _cmd_prefix = f'bash {oop}/'
ci = OOPShell(command=script_name)
ci.run()

class OOPBadShell(nib.CommandLine):
    _cmd_prefix = f'shell_dne {oop}/'
ci = OOPBadShell(command=script_name)
with pytest.raises(IOError):
    ci.run()
```

## Next Steps


---

*Source: test_core.py:551 | Complexity: Advanced | Last updated: 2026-05-18*