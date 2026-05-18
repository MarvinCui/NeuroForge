# pymc Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_make_obs_var

- Kind: `test-workflow`
- Source: `pymc/tests/model/test_core.py:629`
- Note: Workflow: Check returned values for `data` given known inputs to `as_tensor()`. Note that ndarrays should return a TensorConstant and sparse inputs should return a Sparse PyTensor object.

```python
'\n    Check returned values for `data` given known inputs to `as_tensor()`.\n\n    Note that ndarrays should return a TensorConstant and sparse inputs\n    should return a Sparse PyTensor object.\n    '
input_name = 'testing_inputs'
sparse_input = sps.csr_matrix(np.eye(3))
dense_input = np.arange(9).reshape((3, 3))
masked_array_input = ma.array(dense_input, mask=np.mod(dense_input, 2) == 0)
fake_model = pm.Model()
with fake_model:
    fake_distribution = pm.Normal.dist(mu=0, sigma=1, size=(3, 3))
    fake_distribution.name = input_name
with pytest.raises(ShapeError, match="Dimensionality of data and RV don't match."):
    fake_model.make_obs_var(fake_distribution, np.ones((3, 3, 1)), None, None, None, None)
dense_output = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, None)
assert dense_output == fake_distribution
assert isinstance(fake_model.rvs_to_values[dense_output], TensorConstant)
del fake_model.named_vars[fake_distribution.name]
sparse_output = fake_model.make_obs_var(fake_distribution, sparse_input, None, None, None, None)
assert sparse_output == fake_distribution
assert sparse.basic._is_sparse_variable(fake_model.rvs_to_values[sparse_output])
del fake_model.named_vars[fake_distribution.name]
with pytest.warns(ImputationWarning):
    masked_output = fake_model.make_obs_var(fake_distribution, masked_array_input, None, None, None, None)
assert masked_output != fake_distribution
assert not isinstance(masked_output, RandomVariable)
assert {'testing_inputs_unobserved'} == {v.name for v in fake_model.value_vars}
assert {'testing_inputs', 'testing_inputs_observed'} == {v.name for v in fake_model.observed_RVs}
del fake_model.named_vars[fake_distribution.name]
scaled_outputs = fake_model.make_obs_var(fake_distribution, dense_input, None, None, None, total_size=100)
assert scaled_outputs != fake_distribution
assert isinstance(scaled_outputs.owner.op, MinibatchRandomVariable)
del fake_model.named_vars[fake_distribution.name]
```

## 2. test_autodetect_coords_from_model

- Kind: `test-workflow`
- Source: `pymc/tests/backends/test_arviz.py:257`
- Note: Workflow: test autodetect coords from model

```python
pd = pytest.importorskip('pandas')
df_data = pd.DataFrame(columns=['date']).set_index('date')
dates = pd.date_range(start='2020-05-01', end='2020-05-20')
for city, mu in {'Berlin': 15, 'San Marino': 18, 'Paris': 16}.items():
    df_data[city] = np.random.normal(loc=mu, size=len(dates))
df_data.index = dates
df_data.index.name = 'date'
coords = {'date': df_data.index, 'city': df_data.columns}
with pm.Model(coords=coords) as model:
    europe_mean = pm.Normal('europe_mean_temp', mu=15.0, sigma=3.0)
    city_offset = pm.Normal('city_offset', mu=0.0, sigma=3.0, dims='city')
    city_temperature = pm.Deterministic('city_temperature', europe_mean + city_offset, dims='city')
    data_dims = ('date', 'city')
    data = pm.Data('data', df_data, dims=data_dims)
    _ = pm.Normal('likelihood', mu=city_temperature, sigma=0.5, observed=data, dims=data_dims)
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        trace = pm.sample(return_inferencedata=False, compute_convergence_checks=False, cores=1, chains=1, tune=20, draws=30, step=pm.Metropolis())
    if use_context:
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
            idata = to_inference_data(trace=trace)
if not use_context:
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'More chains .* than draws.*', UserWarning)
        idata = to_inference_data(trace=trace, model=model)
assert 'city' in list(idata.posterior.dims)
assert 'city' in list(idata.observed_data.dims)
assert 'date' in list(idata.observed_data.dims)
np.testing.assert_array_equal(idata.posterior.coords['city'], coords['city'])
np.testing.assert_array_equal(idata.observed_data.coords['date'], coords['date'])
np.testing.assert_array_equal(idata.observed_data.coords['city'], coords['city'])
```

## 3. test_sample_return_lengths

- Kind: `test-workflow`
- Source: `pymc/tests/sampling/test_mcmc.py:349`
- Note: Workflow: test sample return lengths

```python
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

## 4. test_step_args

- Kind: `test-workflow`
- Source: `pymc/tests/sampling/test_mcmc.py:686`
- Note: Workflow: test step args

```python
def accept(idata):
    stats = idata.sample_stats
    return stats.acceptance_rate if 'acceptance_rate' in stats else stats.mean_tree_accept
with pm.Model() as model:
    a = pm.Normal('a')
    idata_default = pm.sample(random_seed=1410)
    idata0 = pm.sample(target_accept=0.5, random_seed=1410)
    idata1 = pm.sample(nuts={'target_accept': 0.5}, random_seed=1410 * 2)
    idata2 = pm.sample(target_accept=0.5, nuts={'max_treedepth': 10}, random_seed=1410)
    with pytest.raises(ValueError, match='`target_accept` was defined twice.'):
        pm.sample(target_accept=0.5, nuts={'target_accept': 0.95}, random_seed=1410)
assert accept(idata_default).mean() > 0.6
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata2).mean(), 0.5, decimal=1)
with pm.Model() as model:
    a = pm.Normal('a')
    b = pm.Poisson('b', 1)
    idata0 = pm.sample(target_accept=0.5, random_seed=1418)
    with warnings.catch_warnings():
        warnings.filterwarnings('ignore', 'invalid value encountered in double_scalars', RuntimeWarning)
        idata1 = pm.sample(nuts={'target_accept': 0.5}, metropolis={'scaling': 0}, random_seed=1418 * 2)
npt.assert_almost_equal(accept(idata0).mean(), 0.5, decimal=1)
npt.assert_almost_equal(accept(idata1).mean(), 0.5, decimal=1)
npt.assert_allclose(idata1.sample_stats.scaling, 0)
```

## 5. test_interdependent_transformed_rvs

- Kind: `test-workflow`
- Source: `pymc/tests/logprob/test_utils.py:210`
- Note: Workflow: test interdependent transformed rvs

```python
with pm.Model() as m:
    transform = pm.distributions.transforms.Interval(bounds_fn=lambda *inputs: (inputs[-2], inputs[-1]))
    x = pm.Uniform('x', lower=0, upper=1, default_transform=transform)
    y = pm.Uniform('y', lower=0, upper=pt.exp(x), default_transform=transform)
    z = pm.Uniform('z', lower=0, upper=y, default_transform=transform)
    w = pm.Uniform('w', lower=0, upper=pt.square(z), default_transform=transform)
rvs = [x, y, z, w]
if reversed:
    rvs = rvs[::-1]
transform_values = replace_rvs_by_values(rvs, rvs_to_values=m.rvs_to_values, rvs_to_transforms=m.rvs_to_transforms)
assert_no_rvs(transform_values)
assert not any(list(explicit_graph_inputs(rvs)))
if reversed:
    transform_values = transform_values[::-1]
transform_values_fn = m.compile_fn(transform_values)
x_interval_test_value = np.random.rand()
y_interval_test_value = np.random.rand()
z_interval_test_value = np.random.rand()
w_interval_test_value = np.random.rand()
expected_x = transform.backward(x_interval_test_value, None, None, None, 0, 1).eval()
expected_y = transform.backward(y_interval_test_value, None, None, None, 0, pt.exp(expected_x)).eval()
expected_z = transform.backward(z_interval_test_value, None, None, None, 0, expected_y).eval()
expected_w = transform.backward(w_interval_test_value, None, None, None, 0, pt.square(expected_z)).eval()
np.testing.assert_allclose(transform_values_fn({'x_interval__': x_interval_test_value, 'y_interval__': y_interval_test_value, 'z_interval__': z_interval_test_value, 'w_interval__': w_interval_test_value}), [expected_x, expected_y, expected_z, expected_w])
```

## 6. test_overwrite_model_coords_dims

- Kind: `test-workflow`
- Source: `pymc/tests/backends/test_arviz.py:307`
- Note: Workflow: Check coords and dims from model object can be partially overwritten.

```python
'Check coords and dims from model object can be partially overwritten.'
dim1 = ['a', 'b']
new_dim1 = ['c', 'd']
coords = {'dim1': dim1, 'dim2': ['c1', 'c2']}
x_data = np.arange(4).reshape((2, 2))
y = x_data + np.random.normal(size=(2, 2))
with pm.Model(coords=coords):
    x = pm.Data('x', x_data, dims=('dim1', 'dim2'))
    beta = pm.Normal('beta', 0, 1, dims='dim1')
    _ = pm.Normal('obs', x * beta, 1, observed=y, dims=('dim1', 'dim2'))
    with pytest.warns(FutureWarning, match='return_inferencedata=False'):
        trace = pm.sample(100, tune=100, return_inferencedata=False)
    idata1 = to_inference_data(trace)
    idata2 = to_inference_data(trace, coords={'dim1': new_dim1}, dims={'beta': ['dim2']})
test_dict = {'posterior': ['beta'], 'observed_data': ['obs'], 'constant_data': ['x']}
fails1 = check_multiple_attrs(test_dict, idata1)
assert not fails1
fails2 = check_multiple_attrs(test_dict, idata2)
assert not fails2
assert 'dim1' in list(idata1.posterior.beta.dims)
assert 'dim2' in list(idata2.posterior.beta.dims)
assert np.all(idata1.constant_data.x.dim1.values == np.array(dim1))
assert np.all(idata1.constant_data.x.dim2.values == np.array(['c1', 'c2']))
assert np.all(idata2.constant_data.x.dim1.values == np.array(new_dim1))
assert np.all(idata2.constant_data.x.dim2.values == np.array(['c1', 'c2']))
```

## 7. test_model_to_graphviz_for_model_with_data_container

- Kind: `test-workflow`
- Source: `pymc/tests/test_data.py:270`
- Note: Workflow: test model to graphviz for model with data container

```python
with pm.Model() as model:
    x = pm.Data('x', [1.0, 2.0, 3.0])
    y = pm.Data('y', [1.0, 2.0, 3.0])
    beta = pm.Normal('beta', 0, 10.0)
    obs_sigma = floatX(np.sqrt(0.01))
    pm.Normal('obs', beta * x, obs_sigma, observed=y)
    pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
for formatting in {'latex', 'latex_with_params'}:
    with pytest.raises(ValueError, match='Unsupported formatting'):
        pm.model_to_graphviz(model, formatting=formatting)
exp_without = ['x [label="x\n~\\Data" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal"]', 'obs [label="obs\n~\nNormal" style=filled]']
exp_with = ['x [label="x\n~\nData" shape=box style="rounded, filled"]', 'y [label="x\n~\nData" shape=box style="rounded, filled"]', 'beta [label="beta\n~\nNormal(mu=0.0, sigma=10.0)"]', f'obs [label="obs\n~\nNormal(mu=f(f(beta), x), sigma={obs_sigma})" style=filled]']
for formatting, expected_substrings in [('plain', exp_without), ('plain_with_params', exp_with)]:
    g = pm.model_to_graphviz(model, formatting=formatting)
    for expected in expected_substrings:
        assert expected in g.source
pm.model_to_graphviz(model, save=tmp_path / 'model.png')
assert path.exists(tmp_path / 'model.png')
pm.model_to_graphviz(model, save=tmp_path / 'a_model', dpi=100)
assert path.exists(tmp_path / 'a_model.png')
```

## 8. test_fgraph_rewrite

- Kind: `test-workflow`
- Source: `pymc/tests/model/test_fgraph.py:341`
- Note: Workflow: Test we can apply a simple rewrite to a PyMC Model.

```python
'Test we can apply a simple rewrite to a PyMC Model.'
with pm.Model(coords={'subject': range(10)}) as m_old:
    group_mean = pm.Normal('group_mean')
    group_std = pm.HalfNormal('group_std')
    subject_mean = pm.Normal('subject_mean', group_mean, group_std, dims=('subject',))
    obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10), dims=('subject',))
fg, _ = fgraph_from_model(m_old)
non_centered_rewrite.apply(fg)
m_new = model_from_fgraph(fg)
assert m_new.named_vars_to_dims == {'subject_mean': ['subject'], 'subject_mean_raw_': ['subject'], 'obs': ['subject']}
assert set(m_new.named_vars) == {'group_mean', 'group_std', 'subject_mean_raw_', 'subject_mean', 'obs'}
assert {rv.name for rv in m_new.free_RVs} == {'group_mean', 'group_std', 'subject_mean_raw_'}
assert {rv.name for rv in m_new.observed_RVs} == {'obs'}
assert {rv.name for rv in m_new.deterministics} == {'subject_mean'}
with pm.Model() as m_ref:
    group_mean = pm.Normal('group_mean')
    group_std = pm.HalfNormal('group_std')
    subject_mean_raw = pm.Normal('subject_mean_raw_', 0, 1, shape=(10,))
    subject_mean = pm.Deterministic('subject_mean', group_mean + subject_mean_raw * group_std)
    obs = pm.Normal('obs', subject_mean, 1, observed=np.zeros(10))
np.testing.assert_array_equal(pm.draw(m_new['subject_mean_raw_'], draws=7, random_seed=1), pm.draw(m_ref['subject_mean_raw_'], draws=7, random_seed=1))
ip = m_new.initial_point()
np.testing.assert_equal(m_new.compile_logp()(ip), m_ref.compile_logp()(ip))
```

## 9. test_get_value_vars_from_user_vars

- Kind: `test-workflow`
- Source: `pymc/tests/test_util.py:228`
- Note: Workflow: test get value vars from user vars

```python
with pm.Model() as model1:
    x1 = pm.Normal('x1', mu=0, sigma=1)
    y1 = pm.Normal('y1', mu=0, sigma=1)
x1_value = model1.rvs_to_values[x1]
y1_value = model1.rvs_to_values[y1]
assert get_value_vars_from_user_vars([x1, y1], model1) == [x1_value, y1_value]
assert get_value_vars_from_user_vars([x1], model1) == [x1_value]
assert get_value_vars_from_user_vars(x1_value, model1) == [x1_value]
assert get_value_vars_from_user_vars([], model1) == []
with pm.Model() as model2:
    x2 = pm.Normal('x2', mu=0, sigma=1)
    y2 = pm.Normal('y2', mu=0, sigma=1)
    det2 = pm.Deterministic('det2', x2 + y2)
prefix = 'The following variables are not random variables in the model:'
with pytest.raises(ValueError, match=f"{prefix} \\['x2', 'y2'\\]"):
    get_value_vars_from_user_vars([x2, y2], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['x2'\\]"):
    get_value_vars_from_user_vars([x2, y1], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['x2'\\]"):
    get_value_vars_from_user_vars([x2], model1)
with pytest.raises(ValueError, match=f"{prefix} \\['det2'\\]"):
    get_value_vars_from_user_vars([det2], model2)
```

## 10. test_censored_workflow

- Kind: `test-workflow`
- Source: `pymc/tests/distributions/test_censored.py:27`
- Note: Workflow: test censored workflow

```python
rng = np.random.default_rng(1234)
size = 500
true_mu = 13.0
true_sigma = 5.0
low = 3.0
high = 16.0
data = rng.normal(true_mu, true_sigma, size)
data[data <= low] = low
data[data >= high] = high
rng = 17092021
with pm.Model() as m:
    mu = pm.Normal('mu', mu=(high - low) / 2 + low, sigma=(high - low) / 2.0, initval='support_point')
    sigma = pm.HalfNormal('sigma', sigma=(high - low) / 2.0, initval='support_point')
    observed = pm.Censored('observed', pm.Normal.dist(mu=mu, sigma=sigma), lower=low if censored else None, upper=high if censored else None, observed=data)
    prior_pred = pm.sample_prior_predictive(random_seed=rng)
    posterior = pm.sample(tune=500, draws=500, random_seed=rng)
    posterior_pred = pm.sample_posterior_predictive(posterior, random_seed=rng)
expected = True if censored else False
assert (9 < prior_pred.prior_predictive.mean() < 10) == expected
assert (13 < posterior.posterior['mu'].mean() < 14) == expected
assert (4.5 < posterior.posterior['sigma'].mean() < 5.5) == expected
assert (12 < posterior_pred.posterior_predictive.mean() < 13) == expected
```

## 11. test_scalar_ode_2_param

- Kind: `test-workflow`
- Source: `pymc/tests/ode/test_ode.py:340`
- Note: Workflow: Test running model for a scalar ODE with 2 parameters

```python
'Test running model for a scalar ODE with 2 parameters'

def system(y, t, p):
    return p[0] * np.exp(-p[0] * t) - p[1] * y[0]
times = np.array([0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0, 6.5, 7.0, 7.5])
yobs = np.array([0.31, 0.57, 0.51, 0.55, 0.47, 0.42, 0.38, 0.3, 0.26, 0.22, 0.22, 0.14, 0.14, 0.09, 0.1])[:, np.newaxis]
ode_model = DifferentialEquation(func=system, t0=0, times=times, n_states=1, n_theta=2)
with pm.Model() as model:
    alpha = pm.HalfCauchy('alpha', 1)
    beta = pm.HalfCauchy('beta', 1)
    y0 = pm.LogNormal('y0', 0, 1)
    sigma = pm.HalfCauchy('sigma', 1)
    forward = ode_model(theta=[alpha, beta], y0=[y0])
    y = pm.LogNormal('y', mu=pm.math.log(forward), sigma=sigma, observed=yobs)
    with pytensor.config.change_flags(mode=fast_unstable_sampling_mode):
        with warnings.catch_warnings():
            warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
            warnings.filterwarnings('ignore', 'invalid value encountered in log', RuntimeWarning)
            idata = pm.sample(50, tune=0, chains=1)
assert idata.posterior['alpha'].shape == (1, 50)
assert idata.posterior['beta'].shape == (1, 50)
assert idata.posterior['y0'].shape == (1, 50)
assert idata.posterior['sigma'].shape == (1, 50)
```

## 12. test_tempered_logp_dlogp

- Kind: `test-workflow`
- Source: `pymc/tests/model/test_core.py:494`
- Note: Workflow: test tempered logp dlogp

```python
with pm.Model() as model:
    pm.Normal('x')
    pm.Normal('y', observed=1)
    pm.Potential('z', pt.constant(-1.0, dtype=pytensor.config.floatX))
func = model.logp_dlogp_function(ravel_inputs=ravel_inputs)
func.set_extra_values({})
func_temp = model.logp_dlogp_function(tempered=True, ravel_inputs=ravel_inputs)
func_temp.set_extra_values({})
func_nograd = model.logp_dlogp_function(compute_grads=False, ravel_inputs=ravel_inputs)
func_nograd.set_extra_values({})
func_temp_nograd = model.logp_dlogp_function(tempered=True, compute_grads=False, ravel_inputs=ravel_inputs)
func_temp_nograd.set_extra_values({})
x = np.ones((1,), dtype=func.dtype)
npt.assert_allclose(func(x)[0], func_temp(x)[0])
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func(x)[0])
func_temp.set_weights(np.array([0.0], dtype=func.dtype))
func_temp_nograd.set_weights(np.array([0.0], dtype=func.dtype))
npt.assert_allclose(func(x)[0], 2 * func_temp(x)[0] - 1)
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
func_temp.set_weights(np.array([0.5], dtype=func.dtype))
func_temp_nograd.set_weights(np.array([0.5], dtype=func.dtype))
npt.assert_allclose(func(x)[0], 4 / 3 * (func_temp(x)[0] - 1 / 4))
npt.assert_allclose(func(x)[1], func_temp(x)[1])
npt.assert_allclose(func_nograd(x), func(x)[0])
npt.assert_allclose(func_temp_nograd(x), func_temp(x)[0])
```
