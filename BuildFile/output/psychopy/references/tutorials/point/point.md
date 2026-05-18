# How To: Point

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test point

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy`
- `psychopy.tests`
- `psychopy.visual`
- `numpy`
- `matplotlib`
- `matplotlib`


## Step-by-Step Guide

### Step 1: Assign poly1 = value

```python
poly1 = [(1, 1), (1, -1), (-1, -1), (-1, 1)]
```

**Verification:**
```python
assert helpers.pointInPolygon(0, 0, poly1)
```

### Step 2: Assign poly2 = value

```python
poly2 = [(2, 2), (1, -1), (-1, -1), (-1, 1)]
```

**Verification:**
```python
assert helpers.pointInPolygon(12, 12, poly1) is False
```

### Step 3: Assign matplotlib.__version__ = '0.0'

```python
matplotlib.__version__ = '0.0'
```

**Verification:**
```python
assert helpers.pointInPolygon(0, 0, [(0, 0), (1, 1)]) is False
```

### Step 4: Assign matplotlib.__version__ = mpl_version

```python
matplotlib.__version__ = mpl_version
```

**Verification:**
```python
assert helpers.polygonsOverlap(poly1, poly2)
```

### Step 5: Assign helpers.nxutils = nxutils

```python
helpers.nxutils = nxutils
```

**Verification:**
```python
assert helpers.polygonsOverlap(poly1, poly2)
```

### Step 6: Assign matplotlib.__version__ = '1.1'

```python
matplotlib.__version__ = '1.1'
```

**Verification:**
```python
assert helpers.polygonsOverlap(poly1, poly2)
```


## Complete Example

```python
# Workflow
poly1 = [(1, 1), (1, -1), (-1, -1), (-1, 1)]
poly2 = [(2, 2), (1, -1), (-1, -1), (-1, 1)]
assert helpers.pointInPolygon(0, 0, poly1)
assert helpers.pointInPolygon(12, 12, poly1) is False
assert helpers.pointInPolygon(0, 0, [(0, 0), (1, 1)]) is False
if have_nxutils:
    helpers.nxutils = nxutils
    matplotlib.__version__ = '1.1'
    assert helpers.polygonsOverlap(poly1, poly2)
    del helpers.nxutils
matplotlib.__version__ = '0.0'
assert helpers.polygonsOverlap(poly1, poly2)
matplotlib.__version__ = mpl_version
```

## Next Steps


---

*Source: test_contains_overlaps.py:138 | Complexity: Intermediate | Last updated: 2026-05-18*