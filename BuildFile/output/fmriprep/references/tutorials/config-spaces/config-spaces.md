# How To: Config Spaces

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that all necessary spaces are recorded in the config.

## Prerequisites

**Required Modules:**
- `os`
- `unittest.mock`
- `pytest`
- `niworkflows.utils.spaces`
- `toml`
- `importlib`


## Step-by-Step Guide

### Step 1: 'Check that all necessary spaces are recorded in the config.'

```python
'Check that all necessary spaces are recorded in the config.'
```

**Verification:**
```python
assert 'MNI152NLin6Asym:res-1' not in [str(s) for s in spaces.get_standard(full_spec=True)]
```

### Step 2: Assign settings = loads(...)

```python
settings = loads(data.load.readable('tests/config.toml').read_text())
```

**Verification:**
```python
assert 'MNI152NLin6Asym_res-1' not in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
```

### Step 3: Call config.nipype.init()

```python
config.nipype.init()
```

**Verification:**
```python
assert 'MNI152NLin6Asym:res-1' in [str(s) for s in spaces.get_standard(full_spec=True)]
```

### Step 4: Call config.loggers.init()

```python
config.loggers.init()
```

**Verification:**
```python
assert 'MNI152NLin6Asym_res-1' in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
```

### Step 5: Call config.init_spaces()

```python
config.init_spaces()
```

**Verification:**
```python
assert [str(s) for s in spaces.get_standard(full_spec=True)] == []
```

### Step 6: Assign spaces = value

```python
spaces = config.workflow.spaces
```

**Verification:**
```python
assert [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3] == ['MNI152NLin2009cAsym']
```

### Step 7: Assign config.workflow.cifti_output = True

```python
config.workflow.cifti_output = True
```

### Step 8: Call config.init_spaces()

```python
config.init_spaces()
```

### Step 9: Assign spaces = value

```python
spaces = config.workflow.spaces
```

**Verification:**
```python
assert 'MNI152NLin6Asym:res-1' in [str(s) for s in spaces.get_standard(full_spec=True)]
```

### Step 10: Assign config.execution.output_spaces = None

```python
config.execution.output_spaces = None
```

### Step 11: Assign config.workflow.cifti_output = False

```python
config.workflow.cifti_output = False
```

### Step 12: Call config.init_spaces()

```python
config.init_spaces()
```

### Step 13: Assign spaces = value

```python
spaces = config.workflow.spaces
```

**Verification:**
```python
assert [str(s) for s in spaces.get_standard(full_spec=True)] == []
```

### Step 14: Call _reset_config()

```python
_reset_config()
```

### Step 15: Assign section = getattr(...)

```python
section = getattr(config, sectionname)
```

### Step 16: Call section.load()

```python
section.load(configs, init=False)
```


## Complete Example

```python
# Workflow
'Check that all necessary spaces are recorded in the config.'
settings = loads(data.load.readable('tests/config.toml').read_text())
for sectionname, configs in settings.items():
    if sectionname != 'environment':
        section = getattr(config, sectionname)
        section.load(configs, init=False)
config.nipype.init()
config.loggers.init()
config.init_spaces()
spaces = config.workflow.spaces
assert 'MNI152NLin6Asym:res-1' not in [str(s) for s in spaces.get_standard(full_spec=True)]
assert 'MNI152NLin6Asym_res-1' not in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
config.workflow.cifti_output = True
config.init_spaces()
spaces = config.workflow.spaces
assert 'MNI152NLin6Asym:res-1' in [str(s) for s in spaces.get_standard(full_spec=True)]
assert 'MNI152NLin6Asym_res-1' in [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3]
config.execution.output_spaces = None
config.workflow.cifti_output = False
config.init_spaces()
spaces = config.workflow.spaces
assert [str(s) for s in spaces.get_standard(full_spec=True)] == []
assert [format_reference((s.fullname, s.spec)) for s in spaces.references if s.standard and s.dim == 3] == ['MNI152NLin2009cAsym']
_reset_config()
```

## Next Steps


---

*Source: test_config.py:59 | Complexity: Advanced | Last updated: 2026-05-18*