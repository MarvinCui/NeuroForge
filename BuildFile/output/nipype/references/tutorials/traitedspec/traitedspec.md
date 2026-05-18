# How To: Traitedspec

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TraitedSpec

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

### Step 1: Assign specfunc = value

```python
specfunc = lambda x: spec(hoo=x)
```

**Verification:**
```python
assert nib.TraitedSpec().get_hashval()
```

### Step 2: Assign infields = spec(...)

```python
infields = spec(foo=1)
```

**Verification:**
```python
assert nib.TraitedSpec().__repr__() == '\n\n'
```

### Step 3: Assign hashval = value

```python
hashval = ([('foo', 1), ('goo', '0.0000000000')], 'e89433b8c9141aa0fda2f8f4d662c047')
```

**Verification:**
```python
assert spec().foo == Undefined
```

### Step 4: Assign foo = value

```python
foo = nib.traits.Int
```

**Verification:**
```python
assert spec().goo == 0.0
```

### Step 5: Assign goo = nib.traits.Float(...)

```python
goo = nib.traits.Float(usedefault=True)
```

**Verification:**
```python
assert infields.get_hashval() == hashval
```

### Step 6: Call specfunc()

```python
specfunc(1)
```

**Verification:**
```python
assert infields.__repr__() == '\nfoo = 1\ngoo = 0.0\n'
```


## Complete Example

```python
# Workflow
assert nib.TraitedSpec().get_hashval()
assert nib.TraitedSpec().__repr__() == '\n\n'

class spec(nib.TraitedSpec):
    foo = nib.traits.Int
    goo = nib.traits.Float(usedefault=True)
assert spec().foo == Undefined
assert spec().goo == 0.0
specfunc = lambda x: spec(hoo=x)
with pytest.raises(nib.traits.TraitError):
    specfunc(1)
infields = spec(foo=1)
hashval = ([('foo', 1), ('goo', '0.0000000000')], 'e89433b8c9141aa0fda2f8f4d662c047')
assert infields.get_hashval() == hashval
assert infields.__repr__() == '\nfoo = 1\ngoo = 0.0\n'
```

## Next Steps


---

*Source: test_specs.py:29 | Complexity: Intermediate | Last updated: 2026-05-18*