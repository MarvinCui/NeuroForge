# How To: Convert To Traits Type

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test convert to traits type

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

### Step 1: Assign Params = namedtuple(...)

```python
Params = namedtuple('Params', 'traits_type is_file')
```

**Verification:**
```python
assert isinstance(trait_instance, res.traits_type)
```

### Step 2: Assign Res = namedtuple(...)

```python
Res = namedtuple('Res', 'traits_type subtype is_mandatory')
```

**Verification:**
```python
assert isinstance(trait_instance.inner_traits()[0].trait_type, res.subtype)
```

### Step 3: Assign l_entries = value

```python
l_entries = [Params('variable string', False), Params('variable int', False), Params('variable float', False), Params('variable bool', False), Params('variable complex', False), Params('variable int, optional', False), Params('variable string, optional', False), Params('variable float, optional', False), Params('variable bool, optional', False), Params('variable complex, optional', False), Params('string', False), Params('int', False), Params('string', True), Params('float', False), Params('bool', False), Params('complex', False), Params('string, optional', False), Params('int, optional', False), Params('string, optional', True), Params('float, optional', False), Params('bool, optional', False), Params('complex, optional', False)]
```

**Verification:**
```python
assert is_mandatory == res.is_mandatory
```

### Step 4: Assign l_expected = value

```python
l_expected = [Res(traits.List, traits.Str, True), Res(traits.List, traits.Int, True), Res(traits.List, traits.Float, True), Res(traits.List, traits.Bool, True), Res(traits.List, traits.Complex, True), Res(traits.List, traits.Int, False), Res(traits.List, traits.Str, False), Res(traits.List, traits.Float, False), Res(traits.List, traits.Bool, False), Res(traits.List, traits.Complex, False), Res(traits.Str, None, True), Res(traits.Int, None, True), Res(File, None, True), Res(traits.Float, None, True), Res(traits.Bool, None, True), Res(traits.Complex, None, True), Res(traits.Str, None, False), Res(traits.Int, None, False), Res(File, None, False), Res(traits.Float, None, False), Res(traits.Bool, None, False), Res(traits.Complex, None, False)]
```

### Step 5: Assign unknown = convert_to_traits_type(...)

```python
traits_type, is_mandatory = convert_to_traits_type(entry.traits_type, entry.is_file)
```

### Step 6: Assign trait_instance = traits_type(...)

```python
trait_instance = traits_type()
```

**Verification:**
```python
assert isinstance(trait_instance, res.traits_type)
```

### Step 7: Call convert_to_traits_type()

```python
convert_to_traits_type('file, optional')
```

**Verification:**
```python
assert isinstance(trait_instance.inner_traits()[0].trait_type, res.subtype)
```


## Complete Example

```python
# Workflow
Params = namedtuple('Params', 'traits_type is_file')
Res = namedtuple('Res', 'traits_type subtype is_mandatory')
l_entries = [Params('variable string', False), Params('variable int', False), Params('variable float', False), Params('variable bool', False), Params('variable complex', False), Params('variable int, optional', False), Params('variable string, optional', False), Params('variable float, optional', False), Params('variable bool, optional', False), Params('variable complex, optional', False), Params('string', False), Params('int', False), Params('string', True), Params('float', False), Params('bool', False), Params('complex', False), Params('string, optional', False), Params('int, optional', False), Params('string, optional', True), Params('float, optional', False), Params('bool, optional', False), Params('complex, optional', False)]
l_expected = [Res(traits.List, traits.Str, True), Res(traits.List, traits.Int, True), Res(traits.List, traits.Float, True), Res(traits.List, traits.Bool, True), Res(traits.List, traits.Complex, True), Res(traits.List, traits.Int, False), Res(traits.List, traits.Str, False), Res(traits.List, traits.Float, False), Res(traits.List, traits.Bool, False), Res(traits.List, traits.Complex, False), Res(traits.Str, None, True), Res(traits.Int, None, True), Res(File, None, True), Res(traits.Float, None, True), Res(traits.Bool, None, True), Res(traits.Complex, None, True), Res(traits.Str, None, False), Res(traits.Int, None, False), Res(File, None, False), Res(traits.Float, None, False), Res(traits.Bool, None, False), Res(traits.Complex, None, False)]
for entry, res in zip(l_entries, l_expected):
    traits_type, is_mandatory = convert_to_traits_type(entry.traits_type, entry.is_file)
    trait_instance = traits_type()
    assert isinstance(trait_instance, res.traits_type)
    if res.subtype:
        assert isinstance(trait_instance.inner_traits()[0].trait_type, res.subtype)
    assert is_mandatory == res.is_mandatory
with pytest.raises(IOError):
    convert_to_traits_type('file, optional')
```

## Next Steps


---

*Source: test_base.py:17 | Complexity: Advanced | Last updated: 2026-05-18*