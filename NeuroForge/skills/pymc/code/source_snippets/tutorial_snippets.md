# pymc Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Make Obs Var

- Kind: `tutorial`
- Source: `references/tutorials/make-obs-var/make-obs-var.md`
- Note: Workflow: Check returned values for `data` given known inputs to `as_tensor()`. Note that ndarrays should return a TensorConstant and sparse inputs should return a Sparse PyTensor object.

```python
# Workflow
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

## 2. How To: Autodetect Coords From Model

- Kind: `tutorial`
- Source: `references/tutorials/autodetect-coords-from-model/autodetect-coords-from-model.md`
- Note: Workflow: test autodetect coords from model

```python
# Setup
# Fixtures: use_context

# Workflow
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

## 3. How To: Sample Return Lengths

- Kind: `tutorial`
- Source: `references/tutorials/sample-return-lengths/sample-return-lengths.md`
- Note: Workflow: test sample return lengths

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

## 4. How To: Model To Graphviz For Model With Data Container

- Kind: `tutorial`
- Source: `references/tutorials/model-to-graphviz-for-model-with-data-container/model-to-graphviz-for-model-with-data-container.md`
- Note: Workflow: test model to graphviz for model with data container

```python
# Setup
# Fixtures: tmp_path

# Workflow
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

## 5. How To: Step Args

- Kind: `tutorial`
- Source: `references/tutorials/step-args/step-args.md`
- Note: Workflow: test step args

```python
# Workflow
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

## 6. How To: Interdependent Transformed Rvs

- Kind: `tutorial`
- Source: `references/tutorials/interdependent-transformed-rvs/interdependent-transformed-rvs.md`
- Note: Workflow: test interdependent transformed rvs

```python
# Setup
# Fixtures: reversed

# Workflow
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

## 7. How To: Keep Warning Stat Setting

- Kind: `tutorial`
- Source: `references/tutorials/keep-warning-stat-setting/keep-warning-stat-setting.md`
- Note: Workflow: The ``keep_warning_stat`` stat (aka "Adrian's kwarg) enables users to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group. This breaks ``idata.to_netcdf()`` which is why it defaults to `

```python
# Setup
# Fixtures: keep_warning_stat

# Workflow
'The ``keep_warning_stat`` stat (aka "Adrian\'s kwarg) enables users\n        to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group.\n        This breaks ``idata.to_netcdf()`` which is why it defaults to ``False``.\n        '
sample_kwargs = {'tune': 2, 'draws': 3, 'chains': 1, 'compute_convergence_checks': False, 'discard_tuned_samples': False, 'keep_warning_stat': keep_warning_stat}
if keep_warning_stat:
    sample_kwargs['keep_warning_stat'] = True
with pm.Model():
    pm.Normal('n')
    idata = pm.sample(step=ApocalypticMetropolis(), **sample_kwargs)
if keep_warning_stat:
    assert 'warning' in idata.warmup_sample_stats
    assert 'warning' in idata.sample_stats
    assert 'warning' in idata.sample_stats
    warn_objs = list(idata.sample_stats.warning.sel(chain=0).values.flatten())
    assert warn_objs
    if isinstance(warn_objs[0], np.ndarray):
        warn_objs = [a.tolist() for a in warn_objs]
    assert any((isinstance(w, SamplerWarning) for w in warn_objs))
    assert any(('Asteroid' in w.message for w in warn_objs))
else:
    assert 'warning' not in idata.warmup_sample_stats
    assert 'warning' not in idata.sample_stats
    assert 'warning_dim_0' not in idata.warmup_sample_stats
    assert 'warning_dim_0' not in idata.sample_stats
```

## 8. How To: Overwrite Model Coords Dims

- Kind: `tutorial`
- Source: `references/tutorials/overwrite-model-coords-dims/overwrite-model-coords-dims.md`
- Note: Workflow: Check coords and dims from model object can be partially overwritten.

```python
# Workflow
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

## 9. How To: Scale Cost To Minibatch Works

- Kind: `tutorial`
- Source: `references/tutorials/scale-cost-to-minibatch-works/scale-cost-to-minibatch-works.md`
- Note: Workflow: test scale cost to minibatch works

```python
# Setup
# Fixtures: aux_total_size

# Workflow
mu0 = 1.5
sigma = 1.0
y_obs = np.array([1.6, 1.4])
beta = len(y_obs) / float(aux_total_size)
with pytensor.config.change_flags(floatX='float64', warn_float64='ignore'):
    assert pytensor.config.floatX == 'float64'
    assert pytensor.config.warn_float64 == 'ignore'
    post_mu = np.array([1.88], dtype=pytensor.config.floatX)
    post_sigma = np.array([1], dtype=pytensor.config.floatX)
    with pm.Model():
        mu = pm.Normal('mu', mu=mu0, sigma=sigma)
        pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
        mean_field_1 = MeanField()
        assert mean_field_1.scale_cost_to_minibatch
        mean_field_1.shared_params['mu'].set_value(post_mu)
        mean_field_1.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
        elbo_via_total_size_scaled = -KL(mean_field_1)()(10000)
    with pm.Model():
        mu = pm.Normal('mu', mu=mu0, sigma=sigma)
        pm.Normal('y', mu=mu, sigma=1, observed=y_obs, total_size=aux_total_size)
        mean_field_2 = MeanField()
        assert mean_field_1.scale_cost_to_minibatch
        mean_field_2.scale_cost_to_minibatch = False
        assert not mean_field_2.scale_cost_to_minibatch
        mean_field_2.shared_params['mu'].set_value(post_mu)
        mean_field_2.shared_params['rho'].set_value(np.log(np.exp(post_sigma) - 1))
    elbo_via_total_size_unscaled = -KL(mean_field_2)()(10000)
    np.testing.assert_allclose(elbo_via_total_size_unscaled.eval(), elbo_via_total_size_scaled.eval() * floatX(1 / beta), rtol=0.02, atol=0.1)
```

## 10. How To: Fgraph Rewrite

- Kind: `tutorial`
- Source: `references/tutorials/fgraph-rewrite/fgraph-rewrite.md`
- Note: Workflow: Test we can apply a simple rewrite to a PyMC Model.

```python
# Setup
# Fixtures: non_centered_rewrite

# Workflow
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

## 11. How To: Eager Import Heavy Dependencies

- Kind: `tutorial`
- Source: `references/tutorials/eager-import-heavy-dependencies/eager-import-heavy-dependencies.md`
- Note: Workflow: `import pymc` must not eagerly load heavy optional dependencies. These modules are deferred to first use to keep ``import pymc`` fast. Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it

```python
# Workflow
"`import pymc` must not eagerly load heavy optional dependencies.\n\n    These modules are deferred to first use to keep ``import pymc`` fast.\n    Note: ``scipy.sparse`` is intentionally omitted because ``xarray`` pulls it\n    in transitively, which is outside of pymc's control.\n    "
expensive_modules = ('arviz_base', 'arviz_plots', 'arviz_stats', 'pytensor.sparse', 'scipy.cluster', 'scipy.interpolate', 'scipy.linalg', 'scipy.optimize', 'scipy.spatial', 'scipy.special', 'scipy.stats', 'zarr')
code = textwrap.dedent("        import builtins, sys, traceback\n        _targets = set({targets})\n        _traces, _real = {{}}, builtins.__import__\n        def _hook(name, *a, **kw):\n            if name in _targets and name not in sys.modules and name not in _traces:\n                _traces[name] = ''.join(traceback.format_stack())\n            return _real(name, *a, **kw)\n        builtins.__import__ = _hook\n        import pymc\n        loaded = [m for m in sorted(_targets) if m in sys.modules]\n        print(','.join(loaded))\n        for m in loaded[:3]:\n            print(f'--- {{m}} ---')\n            print(_traces.get(m, '(no trace)'))\n    ").format(targets=expensive_modules)
result = subprocess.run([sys.executable, '-c', code], check=True, capture_output=True, text=True)
lines = result.stdout.strip().split('\n')
loaded = [m for m in lines[0].split(',') if m]
assert not loaded, f'`import pymc` eagerly loaded heavy modules: {loaded}. These should be deferred to first use.\n' + '\n'.join(lines[1:])
```

## 12. How To: Model Table Dims

- Kind: `tutorial`
- Source: `references/tutorials/model-table-dims/model-table-dims.md`
- Note: Workflow: test model table dims

```python
# Workflow
coords = {'subject': range(20), 'param': ['a', 'b']}
with pm.Model(coords=coords) as m:
    x = pmd.Data('x', np.random.normal(size=(20, 2)), dims=('subject', 'param'))
    y_obs_data = pmd.Data('y_obs_data', np.random.normal(size=(20,)), dims='subject')
    beta = pmd.Normal('beta', mu=0, sigma=1, dims='param')
    mu = pmd.Deterministic('mu', (x * beta).sum('param'))
    sigma = pmd.HalfNormal('sigma', sigma=1)
    zsn = pmd.ZeroSumNormal('zsn', sigma=1.0, core_dims='subject')
    pmd.Normal('y_obs', mu=mu + zsn, sigma=sigma, observed=y_obs_data)
    pmd.Potential('beta_penalty', -beta)
text = table_to_text(m.table())
expected = '       Variable  Expression                             Dimensions\n───────────────────────────────────────────────────────────────────────────────\n            x =  Data                                   subject[20] × param[2]\n   y_obs_data =  Data                                   subject[20]\n\n         beta ~  Normal(0, 1)                           param[2]\n        sigma ~  HalfNormal(0, 1)\n          zsn ~  ZeroSumNormal(<constant>, <constant>)  subject[20]\n                                                        Parameter count = 23\n\n           mu =  f(beta, x)                             subject[20]\n\n beta_penalty =  Potential(f(beta))                     param[2]\n\n        y_obs ~  Normal(f(mu, zsn), sigma)              subject[20]\n'
assert [s.rstrip() for s in text.splitlines()] == expected.splitlines()
```
