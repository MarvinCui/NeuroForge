# How To: Create Interface Specs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test create interface specs

## Prerequisites

**Required Modules:**
- `pytest`
- `packaging.version`
- `collections`
- `base`
- `base`
- `dipy.utils.deprecator`
- `dipy.workflows.workflow`
- `dipy.workflows`


## Step-by-Step Guide

### Step 1: Assign new_interface = create_interface_specs(...)

```python
new_interface = create_interface_specs('MyInterface')
```

**Verification:**
```python
assert new_interface.__base__ == TraitedSpec
```

### Step 2: Assign new_interface = create_interface_specs(...)

```python
new_interface = create_interface_specs('MyInterface', BaseClass=BaseInterfaceInputSpec)
```

**Verification:**
```python
assert isinstance(new_interface(), TraitedSpec)
```

### Step 3: Assign params = value

```python
params = [('params1', 'string', ['my description']), ('params2_files', 'string', ['my description @']), ('params3', 'int, optional', ['useful option']), ('out_params', 'string', ['my out description'])]
```

**Verification:**
```python
assert new_interface.__name__ == 'MyInterface'
```

### Step 4: Assign new_interface = create_interface_specs(...)

```python
new_interface = create_interface_specs('MyInterface', params=params, BaseClass=BaseInterfaceInputSpec)
```

**Verification:**
```python
assert not new_interface().get()
```

### Step 5: Assign current_params = new_interface.get(...)

```python
current_params = new_interface().get()
```

**Verification:**
```python
assert new_interface.__base__ == BaseInterfaceInputSpec
```


## Complete Example

```python
# Workflow
new_interface = create_interface_specs('MyInterface')
assert new_interface.__base__ == TraitedSpec
assert isinstance(new_interface(), TraitedSpec)
assert new_interface.__name__ == 'MyInterface'
assert not new_interface().get()
new_interface = create_interface_specs('MyInterface', BaseClass=BaseInterfaceInputSpec)
assert new_interface.__base__ == BaseInterfaceInputSpec
assert isinstance(new_interface(), BaseInterfaceInputSpec)
assert new_interface.__name__ == 'MyInterface'
assert not new_interface().get()
params = [('params1', 'string', ['my description']), ('params2_files', 'string', ['my description @']), ('params3', 'int, optional', ['useful option']), ('out_params', 'string', ['my out description'])]
new_interface = create_interface_specs('MyInterface', params=params, BaseClass=BaseInterfaceInputSpec)
assert new_interface.__base__ == BaseInterfaceInputSpec
assert isinstance(new_interface(), BaseInterfaceInputSpec)
assert new_interface.__name__ == 'MyInterface'
current_params = new_interface().get()
assert len(current_params) == 4
assert 'params1' in current_params
assert 'params2_files' in current_params
assert 'params3' in current_params
assert 'out_params' in current_params
```

## Next Steps


---

*Source: test_base.py:83 | Complexity: Intermediate | Last updated: 2026-05-18*