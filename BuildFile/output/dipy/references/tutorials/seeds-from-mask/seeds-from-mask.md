# How To: Seeds From Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test seeds from mask

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign mask = rng.integers(...)

```python
mask = rng.integers(0, 1, size=(10, 10, 10))
```

**Verification:**
```python
assert_true(np.all((seeds > 2.5) & (seeds < 3.5)))
```

### Step 2: Assign seeds = seeds_from_mask(...)

```python
seeds = seeds_from_mask(mask, np.eye(4), density=1)
```

**Verification:**
```python
assert_true(np.all((seeds > 2.5) & (seeds < 4.5)))
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(mask.sum(), len(seeds))
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(np.argwhere(mask), seeds)
```

### Step 5: Assign unknown = False

```python
mask[:] = False
```

### Step 6: Assign unknown = True

```python
mask[3, 3, 3] = True
```

### Step 7: Assign seeds = seeds_from_mask(...)

```python
seeds = seeds_from_mask(mask, np.eye(4), density=[3, 4, 5])
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(len(seeds), 3 * 4 * 5)
```

### Step 9: Call assert_true()

```python
assert_true(np.all((seeds > 2.5) & (seeds < 3.5)))
```

### Step 10: Assign unknown = True

```python
mask[4, 4, 4] = True
```

### Step 11: Assign seeds = seeds_from_mask(...)

```python
seeds = seeds_from_mask(mask, np.eye(4), density=[3, 4, 5])
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(len(seeds), 2 * 3 * 4 * 5)
```

### Step 13: Call assert_true()

```python
assert_true(np.all((seeds > 2.5) & (seeds < 4.5)))
```

### Step 14: Assign in_333 = unknown.all(...)

```python
in_333 = ((seeds > 2.5) & (seeds < 3.5)).all(1)
```

### Step 15: Call npt.assert_equal()

```python
npt.assert_equal(in_333.sum(), 3 * 4 * 5)
```

### Step 16: Assign in_444 = unknown.all(...)

```python
in_444 = ((seeds > 3.5) & (seeds < 4.5)).all(1)
```

### Step 17: Call npt.assert_equal()

```python
npt.assert_equal(in_444.sum(), 3 * 4 * 5)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
mask = rng.integers(0, 1, size=(10, 10, 10))
seeds = seeds_from_mask(mask, np.eye(4), density=1)
npt.assert_equal(mask.sum(), len(seeds))
npt.assert_array_equal(np.argwhere(mask), seeds)
mask[:] = False
mask[3, 3, 3] = True
seeds = seeds_from_mask(mask, np.eye(4), density=[3, 4, 5])
npt.assert_equal(len(seeds), 3 * 4 * 5)
assert_true(np.all((seeds > 2.5) & (seeds < 3.5)))
mask[4, 4, 4] = True
seeds = seeds_from_mask(mask, np.eye(4), density=[3, 4, 5])
npt.assert_equal(len(seeds), 2 * 3 * 4 * 5)
assert_true(np.all((seeds > 2.5) & (seeds < 4.5)))
in_333 = ((seeds > 2.5) & (seeds < 3.5)).all(1)
npt.assert_equal(in_333.sum(), 3 * 4 * 5)
in_444 = ((seeds > 3.5) & (seeds < 4.5)).all(1)
npt.assert_equal(in_444.sum(), 3 * 4 * 5)
```

## Next Steps


---

*Source: test_utils.py:667 | Complexity: Advanced | Last updated: 2026-05-18*