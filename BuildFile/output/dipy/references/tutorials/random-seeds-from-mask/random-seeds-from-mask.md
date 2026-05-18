# How To: Random Seeds From Mask

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test random seeds from mask

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
mask = rng.integers(0, 1, size=(4, 6, 3))
```

**Verification:**
```python
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
```

### Step 2: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=24, seed_count_per_voxel=True)
```

**Verification:**
```python
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(mask.sum() * 24, len(seeds))
```

**Verification:**
```python
assert_true(np.all(seeds_npv_2 == seeds_npv_3))
```

### Step 4: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=0, seed_count_per_voxel=True)
```

**Verification:**
```python
assert_true(np.all(seeds_nt_150 == seeds_nt_500))
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(0, len(seeds))
```

### Step 6: Assign unknown = False

```python
mask[:] = False
```

### Step 7: Assign unknown = True

```python
mask[2, 2, 2] = True
```

### Step 8: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=8, seed_count_per_voxel=True)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(mask.sum() * 8, len(seeds))
```

### Step 10: Call assert_true()

```python
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
```

### Step 11: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=24, seed_count_per_voxel=False)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(24, len(seeds))
```

### Step 13: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=0, seed_count_per_voxel=False)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(0, len(seeds))
```

### Step 15: Assign unknown = False

```python
mask[:] = False
```

### Step 16: Assign unknown = True

```python
mask[2, 2, 2] = True
```

### Step 17: Assign seeds = random_seeds_from_mask(...)

```python
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=100, seed_count_per_voxel=False)
```

### Step 18: Call npt.assert_equal()

```python
npt.assert_equal(100, len(seeds))
```

### Step 19: Call assert_true()

```python
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
```

### Step 20: Assign mask = np.zeros(...)

```python
mask = np.zeros((15, 15, 15))
```

### Step 21: Assign unknown = 1

```python
mask[2:14, 2:14, 2:14] = 1
```

### Step 22: Assign seeds_npv_2 = value

```python
seeds_npv_2 = random_seeds_from_mask(mask, np.eye(4), seeds_count=2, seed_count_per_voxel=True, random_seed=0)[:150]
```

### Step 23: Assign seeds_npv_3 = value

```python
seeds_npv_3 = random_seeds_from_mask(mask, np.eye(4), seeds_count=3, seed_count_per_voxel=True, random_seed=0)[:150]
```

### Step 24: Call assert_true()

```python
assert_true(np.all(seeds_npv_2 == seeds_npv_3))
```

### Step 25: Assign seeds_nt_150 = value

```python
seeds_nt_150 = random_seeds_from_mask(mask, np.eye(4), seeds_count=150, seed_count_per_voxel=False, random_seed=0)[:150]
```

### Step 26: Assign seeds_nt_500 = value

```python
seeds_nt_500 = random_seeds_from_mask(mask, np.eye(4), seeds_count=500, seed_count_per_voxel=False, random_seed=0)[:150]
```

### Step 27: Call assert_true()

```python
assert_true(np.all(seeds_nt_150 == seeds_nt_500))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
mask = rng.integers(0, 1, size=(4, 6, 3))
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=24, seed_count_per_voxel=True)
npt.assert_equal(mask.sum() * 24, len(seeds))
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=0, seed_count_per_voxel=True)
npt.assert_equal(0, len(seeds))
mask[:] = False
mask[2, 2, 2] = True
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=8, seed_count_per_voxel=True)
npt.assert_equal(mask.sum() * 8, len(seeds))
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=24, seed_count_per_voxel=False)
npt.assert_equal(24, len(seeds))
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=0, seed_count_per_voxel=False)
npt.assert_equal(0, len(seeds))
mask[:] = False
mask[2, 2, 2] = True
seeds = random_seeds_from_mask(mask, np.eye(4), seeds_count=100, seed_count_per_voxel=False)
npt.assert_equal(100, len(seeds))
assert_true(np.all((seeds > 1.5) & (seeds < 2.5)))
mask = np.zeros((15, 15, 15))
mask[2:14, 2:14, 2:14] = 1
seeds_npv_2 = random_seeds_from_mask(mask, np.eye(4), seeds_count=2, seed_count_per_voxel=True, random_seed=0)[:150]
seeds_npv_3 = random_seeds_from_mask(mask, np.eye(4), seeds_count=3, seed_count_per_voxel=True, random_seed=0)[:150]
assert_true(np.all(seeds_npv_2 == seeds_npv_3))
seeds_nt_150 = random_seeds_from_mask(mask, np.eye(4), seeds_count=150, seed_count_per_voxel=False, random_seed=0)[:150]
seeds_nt_500 = random_seeds_from_mask(mask, np.eye(4), seeds_count=500, seed_count_per_voxel=False, random_seed=0)[:150]
assert_true(np.all(seeds_nt_150 == seeds_nt_500))
```

## Next Steps


---

*Source: test_utils.py:690 | Complexity: Advanced | Last updated: 2026-05-18*