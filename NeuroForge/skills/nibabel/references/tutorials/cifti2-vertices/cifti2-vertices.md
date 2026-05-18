# How To: Cifti2 Vertices

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cifti2 vertices

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

### Step 1: Assign vs = ci.Cifti2Vertices(...)

```python
vs = ci.Cifti2Vertices()
```

**Verification:**
```python
assert vs.to_xml() == b'<Vertices BrainStructure="CIFTI_STRUCTURE_OTHER" />'
```

### Step 2: Assign vs.brain_structure = 'CIFTI_STRUCTURE_OTHER'

```python
vs.brain_structure = 'CIFTI_STRUCTURE_OTHER'
```

**Verification:**
```python
assert len(vs) == 0
```

### Step 3: Call vs.extend()

```python
vs.extend(np.array([0, 1, 2]))
```

**Verification:**
```python
assert len(vs) == 3
```

### Step 4: Assign unknown = 10

```python
vs[0] = 10
```

**Verification:**
```python
assert vs.to_xml() == b'<Vertices BrainStructure="CIFTI_STRUCTURE_OTHER">0 1 2</Vertices>'
```

### Step 5: Assign vs = ci.Cifti2Vertices(...)

```python
vs = ci.Cifti2Vertices(vertices=[0, 1, 2])
```

**Verification:**
```python
assert vs[0] == 10
```

### Step 6: Call vs.to_xml()

```python
vs.to_xml()
```

**Verification:**
```python
assert len(vs) == 3
```

### Step 7: Assign unknown = 'a'

```python
vs[1] = 'a'
```

**Verification:**
```python
assert len(vs) == 3
```

### Step 8: Call vs.insert()

```python
vs.insert(1, 'a')
```


## Complete Example

```python
# Workflow
vs = ci.Cifti2Vertices()
with pytest.raises(ci.Cifti2HeaderError):
    vs.to_xml()
vs.brain_structure = 'CIFTI_STRUCTURE_OTHER'
assert vs.to_xml() == b'<Vertices BrainStructure="CIFTI_STRUCTURE_OTHER" />'
assert len(vs) == 0
vs.extend(np.array([0, 1, 2]))
assert len(vs) == 3
with pytest.raises(ValueError):
    vs[1] = 'a'
with pytest.raises(ValueError):
    vs.insert(1, 'a')
assert vs.to_xml() == b'<Vertices BrainStructure="CIFTI_STRUCTURE_OTHER">0 1 2</Vertices>'
vs[0] = 10
assert vs[0] == 10
assert len(vs) == 3
vs = ci.Cifti2Vertices(vertices=[0, 1, 2])
assert len(vs) == 3
```

## Next Steps


---

*Source: test_cifti2.py:199 | Complexity: Advanced | Last updated: 2026-05-18*