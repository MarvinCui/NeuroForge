# How To: Traitedspec Dynamic

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test TraitedSpec dynamic

## Prerequisites

**Required Modules:**
- `os`
- `warnings`
- `pytest`
- `utils.filemanip`
- `base`
- `interfaces`
- `utility.wrappers`
- `pipeline`
- `specs`
- `pickle`


## Step-by-Step Guide

### Step 1: Assign a = nib.BaseTraitedSpec(...)

```python
a = nib.BaseTraitedSpec()
```

### Step 2: Call a.add_trait()

```python
a.add_trait('foo', nib.traits.Int)
```

### Step 3: Assign a.foo = 1

```python
a.foo = 1
```

### Step 4: Assign assign_a = value

```python
assign_a = lambda: setattr(a, 'foo', 'a')
```

### Step 5: Assign pkld_a = dumps(...)

```python
pkld_a = dumps(a)
```

### Step 6: Assign unpkld_a = loads(...)

```python
unpkld_a = loads(pkld_a)
```

### Step 7: Assign assign_a_again = value

```python
assign_a_again = lambda: setattr(unpkld_a, 'foo', 'a')
```

### Step 8: assign_a

```python
assign_a
```

### Step 9: assign_a_again

```python
assign_a_again
```


## Complete Example

```python
# Workflow
from pickle import dumps, loads
a = nib.BaseTraitedSpec()
a.add_trait('foo', nib.traits.Int)
a.foo = 1
assign_a = lambda: setattr(a, 'foo', 'a')
with pytest.raises(Exception):
    assign_a
pkld_a = dumps(a)
unpkld_a = loads(pkld_a)
assign_a_again = lambda: setattr(unpkld_a, 'foo', 'a')
with pytest.raises(Exception):
    assign_a_again
```

## Next Steps


---

*Source: test_specs.py:66 | Complexity: Advanced | Last updated: 2026-05-18*