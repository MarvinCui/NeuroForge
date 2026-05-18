# How To: Sample Return Lengths

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample return lengths

## Prerequisites

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.ndarray`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.sampling.mcmc`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.testing`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign traces = list(...)

```python
traces = list(mtrace._straces.values())
```

**Verification:**
```python
assert isinstance(mtrace, pm.backends.base.MultiTrace)
```

### Step 2: Assign mtrace_pst = pm.sampling.mcmc._sample_return(...)

```python
mtrace_pst = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=True, return_inferencedata=False, compute_convergence_checks=False, keep_warning_stat=True, idata_kwargs={}, model=model)
```

**Verification:**
```python
assert len(mtrace) == 150
```

### Step 3: Assign idata_w = pm.sampling.mcmc._sample_return(...)

```python
idata_w = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=False, compute_convergence_checks=False, return_inferencedata=True, keep_warning_stat=True, idata_kwargs={}, model=model)
```

**Verification:**
```python
assert len(traces) == 3
```

### Step 4: Assign idata = pm.sampling.mcmc._sample_return(...)

```python
idata = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=True, compute_convergence_checks=False, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={}, model=model)
```

**Verification:**
```python
assert isinstance(mtrace_pst, pm.backends.base.MultiTrace)
```

### Step 5: Call pm.Normal()

```python
pm.Normal('n')
```

**Verification:**
```python
assert len(mtrace_pst) == 100
```

### Step 6: Assign mtrace = pm.sample(...)

```python
mtrace = pm.sample(draws=100, tune=50, cores=1, chains=3, step=pm.Metropolis(), return_inferencedata=False, discard_tuned_samples=False)
```

**Verification:**
```python
assert mtrace_pst.report.t_sampling == 123.4
```


## Complete Example

```python
# Workflow
with pm.Model() as model:
    pm.Normal('n')
    with pytest.warns(UserWarning, match='will be included'), pytest.warns(FutureWarning, match='return_inferencedata=False'):
        mtrace = pm.sample(draws=100, tune=50, cores=1, chains=3, step=pm.Metropolis(), return_inferencedata=False, discard_tuned_samples=False)
        assert isinstance(mtrace, pm.backends.base.MultiTrace)
        assert len(mtrace) == 150
traces = list(mtrace._straces.values())
assert len(traces) == 3
mtrace_pst = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=True, return_inferencedata=False, compute_convergence_checks=False, keep_warning_stat=True, idata_kwargs={}, model=model)
assert isinstance(mtrace_pst, pm.backends.base.MultiTrace)
assert len(mtrace_pst) == 100
assert mtrace_pst.report.t_sampling == 123.4
assert mtrace_pst.report.n_tune == 50
assert mtrace_pst.report.n_draws == 100
idata_w = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=False, compute_convergence_checks=False, return_inferencedata=True, keep_warning_stat=True, idata_kwargs={}, model=model)
assert isinstance(idata_w, DataTree)
assert hasattr(idata_w, 'warmup_posterior')
assert idata_w.warmup_posterior.sizes['draw'] == 50
assert idata_w.posterior.sizes['draw'] == 100
assert idata_w.posterior.sizes['chain'] == 3
idata = pm.sampling.mcmc._sample_return(run=None, traces=traces, tune=50, t_sampling=123.4, discard_tuned_samples=True, compute_convergence_checks=False, return_inferencedata=True, keep_warning_stat=False, idata_kwargs={}, model=model)
assert isinstance(idata, DataTree)
assert not hasattr(idata, 'warmup_posterior')
assert idata.posterior.sizes['draw'] == 100
assert idata.posterior.sizes['chain'] == 3
```

## Next Steps


---

*Source: test_mcmc.py:349 | Complexity: Intermediate | Last updated: 2026-05-18*