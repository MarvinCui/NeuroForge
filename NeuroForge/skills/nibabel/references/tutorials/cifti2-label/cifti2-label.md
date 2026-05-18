# How To: Cifti2 Label

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cifti2 label

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

### Step 1: Assign lb = ci.Cifti2Label(...)

```python
lb = ci.Cifti2Label()
```

**Verification:**
```python
assert lb.rgba == (0, 0, 0, 0)
```

### Step 2: Assign lb.label = 'Test'

```python
lb.label = 'Test'
```

**Verification:**
```python
assert compare_xml_leaf(lb.to_xml().decode('utf-8'), "<Label Key='0' Red='0' Green='0' Blue='0' Alpha='0'>Test</Label>")
```

### Step 3: Assign lb.key = 0

```python
lb.key = 0
```

**Verification:**
```python
assert lb.rgba == (0, 0.1, 0.2, 0.3)
```

### Step 4: Assign lb.red = 0

```python
lb.red = 0
```

**Verification:**
```python
assert compare_xml_leaf(lb.to_xml().decode('utf-8'), "<Label Key='0' Red='0' Green='0.1' Blue='0.2' Alpha='0.3'>Test</Label>")
```

### Step 5: Assign lb.green = 0.1

```python
lb.green = 0.1
```

### Step 6: Assign lb.blue = 0.2

```python
lb.blue = 0.2
```

### Step 7: Assign lb.alpha = 0.3

```python
lb.alpha = 0.3
```

**Verification:**
```python
assert lb.rgba == (0, 0.1, 0.2, 0.3)
```

### Step 8: Assign lb.red = 10

```python
lb.red = 10
```

### Step 9: Assign lb.red = 0

```python
lb.red = 0
```

### Step 10: Assign lb.key = 'a'

```python
lb.key = 'a'
```

### Step 11: Assign lb.key = 0

```python
lb.key = 0
```

### Step 12: Call lb.to_xml()

```python
lb.to_xml()
```

### Step 13: Call lb.to_xml()

```python
lb.to_xml()
```


## Complete Example

```python
# Workflow
lb = ci.Cifti2Label()
lb.label = 'Test'
lb.key = 0
assert lb.rgba == (0, 0, 0, 0)
assert compare_xml_leaf(lb.to_xml().decode('utf-8'), "<Label Key='0' Red='0' Green='0' Blue='0' Alpha='0'>Test</Label>")
lb.red = 0
lb.green = 0.1
lb.blue = 0.2
lb.alpha = 0.3
assert lb.rgba == (0, 0.1, 0.2, 0.3)
assert compare_xml_leaf(lb.to_xml().decode('utf-8'), "<Label Key='0' Red='0' Green='0.1' Blue='0.2' Alpha='0.3'>Test</Label>")
lb.red = 10
with pytest.raises(ci.Cifti2HeaderError):
    lb.to_xml()
lb.red = 0
lb.key = 'a'
with pytest.raises(ci.Cifti2HeaderError):
    lb.to_xml()
lb.key = 0
```

## Next Steps


---

*Source: test_cifti2.py:143 | Complexity: Advanced | Last updated: 2026-05-18*