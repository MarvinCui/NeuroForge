# How To: Root Module Not Polluted

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test root module not polluted

## Prerequisites

**Required Modules:**
- `subprocess`
- `sys`
- `textwrap`
- `types`
- `pymc`


## Step-by-Step Guide

### Step 1: Assign actual = value

```python
actual = {name for name in dir(pymc) if not name.startswith('_') and (not isinstance(getattr(pymc, name), types.ModuleType))}
```

**Verification:**
```python
assert not unexpected, f'Unexpected names at pymc root: {sorted(unexpected)}. {hint}'
```

### Step 2: Assign expected = set(...)

```python
expected = set(_EXPLICIT_ROOT_NAMES)
```

**Verification:**
```python
assert not missing, f'Missing names at pymc root: {sorted(missing)}. {hint}'
```

### Step 3: Assign unexpected = value

```python
unexpected = actual - expected
```

### Step 4: Assign missing = value

```python
missing = expected - actual
```

### Step 5: Assign hint = "If a name is intentional, add it to _EXPLICIT_ROOT_NAMES or to the appropriate submodule's __all__. Otherwise, remove the import from pymc/__init__.py."

```python
hint = "If a name is intentional, add it to _EXPLICIT_ROOT_NAMES or to the appropriate submodule's __all__. Otherwise, remove the import from pymc/__init__.py."
```

**Verification:**
```python
assert not unexpected, f'Unexpected names at pymc root: {sorted(unexpected)}. {hint}'
```


## Complete Example

```python
# Workflow
actual = {name for name in dir(pymc) if not name.startswith('_') and (not isinstance(getattr(pymc, name), types.ModuleType))}
expected = set(_EXPLICIT_ROOT_NAMES)
for sub in _REEXPORTED_SUBMODULES:
    expected |= set(_resolve(sub).__all__)
unexpected = actual - expected
missing = expected - actual
hint = "If a name is intentional, add it to _EXPLICIT_ROOT_NAMES or to the appropriate submodule's __all__. Otherwise, remove the import from pymc/__init__.py."
assert not unexpected, f'Unexpected names at pymc root: {sorted(unexpected)}. {hint}'
assert not missing, f'Missing names at pymc root: {sorted(missing)}. {hint}'
```

## Next Steps


---

*Source: test_root_namespace.py:70 | Complexity: Intermediate | Last updated: 2026-05-18*