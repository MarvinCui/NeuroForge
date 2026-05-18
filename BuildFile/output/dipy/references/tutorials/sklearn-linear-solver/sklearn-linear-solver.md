# How To: Sklearn Linear Solver

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sklearn linear solver

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `numpy.testing`
- `scipy.sparse`
- `dipy.core.optimize`
- `dipy.core.optimize`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign MySillySolver = SillySolver(...)

```python
MySillySolver = SillySolver()
```

### Step 2: Assign n_samples = 100

```python
n_samples = 100
```

### Step 3: Assign n_features = 20

```python
n_features = 20
```

### Step 4: Assign y = rng.random(...)

```python
y = rng.random(n_samples)
```

### Step 5: Assign X = np.ones(...)

```python
X = np.ones((n_samples, n_features))
```

### Step 6: Call MySillySolver.fit()

```python
MySillySolver.fit(X, y)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(MySillySolver.coef_, np.ones(n_features))
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(MySillySolver.predict(X), np.ones(n_samples) * 20)
```

### Step 9: Assign self.coef_ = np.ones(...)

```python
self.coef_ = np.ones(X.shape[-1])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
class SillySolver(opt.SKLearnLinearSolver):

    def fit(self, X, y):
        self.coef_ = np.ones(X.shape[-1])
MySillySolver = SillySolver()
n_samples = 100
n_features = 20
y = rng.random(n_samples)
X = np.ones((n_samples, n_features))
MySillySolver.fit(X, y)
npt.assert_equal(MySillySolver.coef_, np.ones(n_features))
npt.assert_equal(MySillySolver.predict(X), np.ones(n_samples) * 20)
```

## Next Steps


---

*Source: test_optimize.py:72 | Complexity: Advanced | Last updated: 2026-05-18*