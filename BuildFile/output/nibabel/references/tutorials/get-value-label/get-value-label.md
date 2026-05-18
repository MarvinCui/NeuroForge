# How To: Get Value Label

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get value label

## Prerequisites

**Required Modules:**
- `logging`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `batteryrunners`
- `casting`
- `spatialimages`
- `volumeutils`
- `wrapstruct`


## Step-by-Step Guide

### Step 1: Assign hdr = MyHdr(...)

```python
hdr = MyHdr()
```

**Verification:**
```python
assert 'improbable' not in hdr.keys()
```

### Step 2: Assign rec = Recoder(...)

```python
rec = Recoder([[0, 'fullness of heart']], ('code', 'label'))
```

**Verification:**
```python
assert hdr.get_value_label(key) == 'fullness of heart'
```

### Step 3: Assign unknown = rec

```python
hdr._field_recoders['improbable'] = rec
```

**Verification:**
```python
assert hdr.get_value_label(key) == f'<unknown code {new_code}>'
```

### Step 4: Assign _field_recoders = value

```python
_field_recoders = {}
```

### Step 5: Call hdr.get_value_label()

```python
hdr.get_value_label('improbable')
```

### Step 6: Call hdr.get_value_label()

```python
hdr.get_value_label('improbable')
```

### Step 7: Assign code = int(...)

```python
code = int(value)
```

### Step 8: Assign rec = Recoder(...)

```python
rec = Recoder([[code, 'fullness of heart']], ('code', 'label'))
```

### Step 9: Assign unknown = rec

```python
hdr._field_recoders[key] = rec
```

**Verification:**
```python
assert hdr.get_value_label(key) == 'fullness of heart'
```

### Step 10: Assign new_code = value

```python
new_code = 1 if code == 0 else 0
```

### Step 11: Assign unknown = new_code

```python
hdr[key] = new_code
```

**Verification:**
```python
assert hdr.get_value_label(key) == f'<unknown code {new_code}>'
```

### Step 12: Call hdr.get_value_label()

```python
hdr.get_value_label(0)
```


## Complete Example

```python
# Workflow
class MyHdr(self.header_class):
    _field_recoders = {}
hdr = MyHdr()
with pytest.raises(ValueError):
    hdr.get_value_label('improbable')
assert 'improbable' not in hdr.keys()
rec = Recoder([[0, 'fullness of heart']], ('code', 'label'))
hdr._field_recoders['improbable'] = rec
with pytest.raises(ValueError):
    hdr.get_value_label('improbable')
for key, value in hdr.items():
    with pytest.raises(ValueError):
        hdr.get_value_label(0)
    if not value.dtype.type in INTEGER_TYPES or not np.isscalar(value):
        continue
    code = int(value)
    rec = Recoder([[code, 'fullness of heart']], ('code', 'label'))
    hdr._field_recoders[key] = rec
    assert hdr.get_value_label(key) == 'fullness of heart'
    new_code = 1 if code == 0 else 0
    hdr[key] = new_code
    assert hdr.get_value_label(key) == f'<unknown code {new_code}>'
```

## Next Steps


---

*Source: test_wrapstruct.py:314 | Complexity: Advanced | Last updated: 2026-05-18*