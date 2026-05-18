# How To: Traitedspec Logic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TraitedSpec logic

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

### Step 1: Assign myif = MyInterface(...)

```python
myif = MyInterface()
```

**Verification:**
```python
assert myif.inputs.foo == 1
```

### Step 2: Assign myif.inputs.foo = 1

```python
myif.inputs.foo = 1
```

**Verification:**
```python
assert myif.inputs.foo == 1
```

### Step 3: Assign set_bar = value

```python
set_bar = lambda: setattr(myif.inputs, 'bar', 1)
```

**Verification:**
```python
assert myif.inputs.kung == 2.0
```

### Step 4: Assign myif.inputs.kung = 2

```python
myif.inputs.kung = 2
```

**Verification:**
```python
assert myif.inputs.kung == 2.0
```

### Step 5: Assign _xor_inputs = value

```python
_xor_inputs = ('foo', 'bar')
```

### Step 6: Assign foo = nib.traits.Int(...)

```python
foo = nib.traits.Int(xor=_xor_inputs, desc='foo or bar, not both')
```

### Step 7: Assign bar = nib.traits.Int(...)

```python
bar = nib.traits.Int(xor=_xor_inputs, desc='bar or foo, not both')
```

### Step 8: Assign kung = nib.traits.Float(...)

```python
kung = nib.traits.Float(requires=('foo',), position=0, desc='kung foo')
```

### Step 9: Assign output = value

```python
output = nib.traits.Int
```

### Step 10: Assign input_spec = spec3

```python
input_spec = spec3
```

### Step 11: Assign output_spec = out3

```python
output_spec = out3
```

### Step 12: Call set_bar()

```python
set_bar()
```


## Complete Example

```python
# Workflow
class spec3(nib.TraitedSpec):
    _xor_inputs = ('foo', 'bar')
    foo = nib.traits.Int(xor=_xor_inputs, desc='foo or bar, not both')
    bar = nib.traits.Int(xor=_xor_inputs, desc='bar or foo, not both')
    kung = nib.traits.Float(requires=('foo',), position=0, desc='kung foo')

class out3(nib.TraitedSpec):
    output = nib.traits.Int

class MyInterface(nib.BaseInterface):
    input_spec = spec3
    output_spec = out3
myif = MyInterface()
myif.inputs.foo = 1
assert myif.inputs.foo == 1
set_bar = lambda: setattr(myif.inputs, 'bar', 1)
with pytest.raises(IOError):
    set_bar()
assert myif.inputs.foo == 1
myif.inputs.kung = 2
assert myif.inputs.kung == 2.0
```

## Next Steps


---

*Source: test_specs.py:117 | Complexity: Advanced | Last updated: 2026-05-18*