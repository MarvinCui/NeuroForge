# How To: Cifti2 Labeltable

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cifti2 labeltable

## Prerequisites

**Required Modules:**
- `collections`
- `xml.etree`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.cifti2.cifti2`
- `nibabel.nifti2`
- `nibabel.tests.test_dataobj_images`
- `nibabel.tests.test_image_api`


## Step-by-Step Guide

### Step 1: Assign lt = ci.Cifti2LabelTable(...)

```python
lt = ci.Cifti2LabelTable()
```

**Verification:**
```python
assert len(lt) == 0
```

### Step 2: Assign label = ci.Cifti2Label(...)

```python
label = ci.Cifti2Label(label='Test', key=0)
```

**Verification:**
```python
assert len(lt) == 1
```

### Step 3: Assign unknown = label

```python
lt[0] = label
```

**Verification:**
```python
assert dict(lt) == {label.key: label}
```

### Step 4: Call lt.clear()

```python
lt.clear()
```

**Verification:**
```python
assert len(lt) == 1
```

### Step 5: Call lt.append()

```python
lt.append(label)
```

**Verification:**
```python
assert dict(lt) == {label.key: label}
```

### Step 6: Call lt.clear()

```python
lt.clear()
```

**Verification:**
```python
assert len(lt) == 1
```

### Step 7: Assign test_tuple = value

```python
test_tuple = (label.label, label.red, label.green, label.blue, label.alpha)
```

**Verification:**
```python
assert (v.label, v.red, v.green, v.blue, v.alpha) == test_tuple
```

### Step 8: Assign unknown = test_tuple

```python
lt[label.key] = test_tuple
```

**Verification:**
```python
assert len(lt) == 1
```

### Step 9: Assign v = value

```python
v = lt[label.key]
```

**Verification:**
```python
assert (v.label, v.red, v.green, v.blue, v.alpha) == test_tuple
```

### Step 10: Call lt.to_xml()

```python
lt.to_xml()
```

### Step 11: Call lt._to_xml_element()

```python
lt._to_xml_element()
```

### Step 12: Assign unknown = label

```python
lt[1] = label
```

### Step 13: Assign unknown = value

```python
lt[0] = test_tuple[:-1]
```

### Step 14: Assign unknown = value

```python
lt[0] = ('foo', 1.1, 0, 0, 1)
```

### Step 15: Assign unknown = value

```python
lt[0] = ('foo', 1.0, -1, 0, 1)
```

### Step 16: Assign unknown = value

```python
lt[0] = ('foo', 1.0, 0, -0.1, 1)
```


## Complete Example

```python
# Workflow
lt = ci.Cifti2LabelTable()
assert len(lt) == 0
with pytest.raises(ci.Cifti2HeaderError):
    lt.to_xml()
with pytest.raises(ci.Cifti2HeaderError):
    lt._to_xml_element()
label = ci.Cifti2Label(label='Test', key=0)
lt[0] = label
assert len(lt) == 1
assert dict(lt) == {label.key: label}
lt.clear()
lt.append(label)
assert len(lt) == 1
assert dict(lt) == {label.key: label}
lt.clear()
test_tuple = (label.label, label.red, label.green, label.blue, label.alpha)
lt[label.key] = test_tuple
assert len(lt) == 1
v = lt[label.key]
assert (v.label, v.red, v.green, v.blue, v.alpha) == test_tuple
with pytest.raises(ValueError):
    lt[1] = label
with pytest.raises(ValueError):
    lt[0] = test_tuple[:-1]
with pytest.raises(ValueError):
    lt[0] = ('foo', 1.1, 0, 0, 1)
with pytest.raises(ValueError):
    lt[0] = ('foo', 1.0, -1, 0, 1)
with pytest.raises(ValueError):
    lt[0] = ('foo', 1.0, 0, -0.1, 1)
```

## Next Steps


---

*Source: test_cifti2.py:102 | Complexity: Advanced | Last updated: 2026-05-18*