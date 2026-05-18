# afni Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_script_imports

- Kind: `test-workflow`
- Source: `afni/tests/scripts/test_python_imports.py:18`
- Note: Workflow: test script imports

```python
if python_interpreter == 'python3':
    pytest.xfail('Not all modules are python3 compatible')
binary_dir = Path(shutil.which('afni')).parent
py_files = list(binary_dir.glob('*.py'))
possible_pymods = [f for f in py_files if not f.name[0] in '@ 1 2 3'.split()]
known_py2 = ['afni_restproc.py', 'afni_skeleton.py', 'afni_xmat.py', 'eg_main_chrono.py', 'fat_mat_sel.py', 'fat_mvm_gridconv.py', 'fat_mvm_prep.py', 'fat_mvm_review.py', 'fat_mvm_scripter.py', 'fat_roi_row.py', 'gui_uber_skel.py', 'gui_xmat.py', 'lib_dti_sundry.py', 'lib_fat_funcs.py', 'lib_fat_plot_sel.py', 'lib_surf_clustsim.py', 'lib_uber_align.py', 'lib_uber_skel.py', 'lpc_align.py', 'make_pq_script.py', 'make_stim_times.py', 'meica.py', 'neuro_deconvolve.py', 'parse_fs_lt_log.py', 'python_module_test.py', 'quick.alpha.vals.py', 'read_matlab_files.py', 'RetroTS.py', 'slow_surf_clustsim.py', 'uber_align_test.py', 'uber_proc.py', 'uber_skel.py', 'ui_xmat.py', 'unWarpEPI.py', 'xmat_tool.py', 'gui_uber_ttest.py', 'gui_uber_align_test.py', 'lib_qt_gui.py', 'gui_uber_subj.py', 'demoExpt.py', 'gui_xmat.py', 'lib_matplot.py', 'lib_RR_plot.py', 'lib_wx.py']
not_importable = ['abids_json_tool.py', 'ClustExp_HistTable.py', 'quick.alpha.vals.py', 'abids_json_info.py', 'tedana_wrapper.py', 'BayesianGroupAna.py', 'abids_tool.py', 'ClustExp_StatParse.py']
other_problems = ['lib_fat_Rfactor.py', 'fat_lat_csv.py']
broken_imports = {}
for script in possible_pymods:
    if script.name in other_problems + not_importable:
        continue
    print(script)
    module_name = script.stem
    try:
        run_cmd(data, "%s -c 'import %s'" % (python_interpreter, module_name), workdir=binary_dir)
    except subprocess.CalledProcessError as e:
        broken_imports[script.name] = e
if broken_imports:
    failed_scripts = ', '.join([p for p in broken_imports.keys()])
    raise ValueError('The following scripts could not be imported: %s' % failed_scripts)
```

## 2. test_examples_parse_correctly

- Kind: `test-workflow`
- Source: `afni/tests/scripts/test_testing_script_functionality.py:964`
- Note: Workflow: test examples parse correctly

```python
monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'dir_path', lambda x: str(Path(x).expanduser()))
stdout_ = sys.stdout
(mocked_script.parent / 'README.rst').write_text('some content')
scripts_dir = mocked_script.parent / 'scripts'
scripts_dir.mkdir()
(scripts_dir / 'test_ptaylor.py').touch()
for name, example in run_tests_examples.examples.items():
    arg_list = shlex.split(example.splitlines()[-1])[1:]
    script_name = name.replace(' ', '_') + '.py'
    example_script = mocked_script.with_name(f'{script_name}')
    example_script.write_text(SCRIPT.read_text())
    monkeypatch.setattr(sys, 'argv', [example_script.name, *arg_list])
    monkeypatch.setattr(afni_test_utils.run_tests_func, 'run_tests', Mock(side_effect=SystemExit(0)))
    monkeypatch.setattr(afni_test_utils.container_execution, 'run_containerized', Mock(side_effect=SystemExit(0)))
    monkeypatch.setattr(afni_test_utils.minimal_funcs_for_run_tests_cli, 'modify_path_and_env_if_not_using_cmake', lambda *args, **kwargs: None)
    res = runpy.run_path(str(example_script))
    with pytest.raises(SystemExit) as err:
        sys.stdout = open(os.devnull, 'w')
        res['main']()
        sys.stdout = stdout_
    assert err.typename == 'SystemExit'
    assert err.value.code == 0
    if 'local' in arg_list:
        res['main'].__globals__['run_tests'].assert_called_once()
    elif 'container' in arg_list:
        res['main'].__globals__['run_containerized'].assert_called_once()
sys.stdout = stdout_
```

## 3. test__check_hdr_points_space

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/nibabel/tests/test_trackvis.py:276`
- Note: Workflow: test check hdr points space

```python
assert_equal(tv._check_hdr_points_space({}, None), None)
assert_equal(tv._check_hdr_points_space({}, 'voxmm'), None)
assert_raises(ValueError, tv._check_hdr_points_space, {}, 'crazy')
hdr = tv.empty_header()
assert_array_equal(hdr['voxel_size'], [0, 0, 0])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [-2, 3, 4]
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [2, 3, 0]
with ErrorWarnings():
    assert_raises(UserWarning, tv._check_hdr_points_space, hdr, 'voxel')
hdr['voxel_size'] = [2, 3, 4]
assert_equal(tv._check_hdr_points_space(hdr, 'voxel'), None)
hdr['voxel_size'] = [2, 3, 4]
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['voxel_order'] = 'RAS'
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([2, 3, 4, 0])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([-2, 3, 4, 1])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
hdr['vox_to_ras'] = np.diag([3, 3, 4, 1])
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
good_aff = np.diag([2, 3, 4, 1])
hdr['vox_to_ras'] = good_aff
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
hdr['voxel_order'] = ''
assert_raises(tv.HeaderError, tv._check_hdr_points_space, hdr, 'rasmm')
good_lps = np.dot(np.diag([-1, -1, 1, 1]), good_aff)
hdr['vox_to_ras'] = good_lps
assert_equal(tv._check_hdr_points_space(hdr, 'rasmm'), None)
```

## 4. test_TimeDelayNodes

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/mdp/test/test_TimeDelayNodes.py:4`
- Note: Workflow: test TimeDelayNodes

```python
x = numx.array([[1, 2, 3], [2, 4, 4], [3, 8, 5], [4, 16, 6], [5, 32, 7]])
node = TimeDelayNode(time_frames=3, gap=2)
slider = TimeDelaySlidingWindowNode(time_frames=3, gap=2)
real_res = [[1, 2, 3, 0, 0, 0, 0, 0, 0], [2, 4, 4, 0, 0, 0, 0, 0, 0], [3, 8, 5, 1, 2, 3, 0, 0, 0], [4, 16, 6, 2, 4, 4, 0, 0, 0], [5, 32, 7, 3, 8, 5, 1, 2, 3]]
real_res = numx.array(real_res)
res = node.execute(x)
assert_array_equal(real_res, res)
slider_res = numx.zeros_like(real_res)
for row_nr in range(x.shape[0]):
    slider_res[row_nr, :] = slider.execute(x[[row_nr], :])
assert_array_equal(real_res, slider_res)
node = TimeDelayNode(time_frames=2, gap=3)
slider = TimeDelaySlidingWindowNode(time_frames=2, gap=3)
real_res = [[1, 2, 3, 0, 0, 0], [2, 4, 4, 0, 0, 0], [3, 8, 5, 0, 0, 0], [4, 16, 6, 1, 2, 3], [5, 32, 7, 2, 4, 4]]
real_res = numx.array(real_res)
res = node.execute(x)
assert_array_equal(real_res, res)
slider_res = numx.zeros_like(real_res)
for row_nr in range(x.shape[0]):
    slider_res[row_nr, :] = slider.execute(x[[row_nr], :])
assert_array_equal(real_res, slider_res)
node = TimeDelayNode(time_frames=4, gap=1)
slider = TimeDelaySlidingWindowNode(time_frames=4, gap=1)
real_res = [[1, 2, 3, 0, 0, 0, 0, 0, 0, 0, 0, 0], [2, 4, 4, 1, 2, 3, 0, 0, 0, 0, 0, 0], [3, 8, 5, 2, 4, 4, 1, 2, 3, 0, 0, 0], [4, 16, 6, 3, 8, 5, 2, 4, 4, 1, 2, 3], [5, 32, 7, 4, 16, 6, 3, 8, 5, 2, 4, 4]]
real_res = numx.array(real_res)
res = node.execute(x)
assert_array_equal(real_res, res)
slider_res = numx.zeros_like(real_res)
for row_nr in range(x.shape[0]):
    slider_res[row_nr, :] = slider.execute(x[[row_nr], :])
assert_array_equal(real_res, slider_res)
```

## 5. test_rewrite_paths_for_line_error

- Kind: `test-workflow`
- Source: `afni/tests/scripts/test_testing_script_functionality.py:617`
- Note: Workflow: If the the stdout or stderr stream output directories returned from get_command_info_dicts

```python
'\n    If the the stdout or stderr stream  output directories returned from get_command_info_dicts\n    '
cmd_info = defaultdict(lambda: '')
cmd_info['outdir'] = '/a/base/path/output_of_tests/output_2020_11_12_154136'
cmd_info['workdir'] = '/a/base/path'
cmd_info['tests_data_dir'] = '/a/base/path'
monkeypatch.setattr(tools, 'get_command_info_dicts', Mock(return_value=[cmd_info, defaultdict(lambda: '')]))
txt = ['/a/base/path/output_of_tests/output_2020_11_12_154142/subdir other text']
with pytest.raises(ValueError):
    modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
cmd_info['outdir'] = '/a/different/base/path/output_of_tests/output_2020_11_12_154136'
with pytest.raises(ValueError):
    modified_line = tools.rewrite_paths_for_cleaner_diffs(data, [txt])
```

## 6. test_scheduler_flow

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/mdp/test/test_pp_local.py:38`
- Note: Workflow: Test local pp scheduler with real Nodes.

```python
'Test local pp scheduler with real Nodes.'
precision = 10 ** (-6)
node1 = mdp.nodes.PCANode(output_dim=20)
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
node3 = mdp.nodes.SFANode(output_dim=10)
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
scheduler = parallel.pp_support.LocalPPScheduler(ncpus=3, max_queue_length=0, verbose=False)
input_dim = 30
scales = numx.linspace(1, 100, num=input_dim)
scale_matrix = mdp.numx.diag(scales)
train_iterables = [numx.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in range(3)]
parallel_flow.train(train_iterables, scheduler=scheduler)
x = mdp.numx.random.random((10, input_dim))
parallel_flow.execute([x for _ in range(8)], scheduler=scheduler)
scheduler.shutdown()
flow.train(train_iterables)
assert parallel_flow[0].tlen == flow[0].tlen
y1 = flow.execute(x)
y2 = parallel_flow.execute(x)
assert_array_almost_equal(abs(y1 - y2), precision)
```

## 7. test_NeuralGasNode

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/mdp/test/test_NeuralGasNode.py:6`
- Note: Workflow: test NeuralGasNode

```python
dim = 10
npoints = 1000
const = _uniform(-100, 100, [dim])
dir = _uniform(-1, 1, [dim])
dir /= utils.norm2(dir)
x = _uniform(-1, 1, [npoints])
data = numx.outer(x, dir) + const
num_nodes = 10
ng = mdp.nodes.NeuralGasNode(start_poss=[data[n, :] for n in range(num_nodes)], max_epochs=10)
ng.train(data)
ng.stop_training()
poss = ng.get_nodes_position() - const
norms = numx.sqrt(numx.sum(poss * poss, axis=1))
poss = (poss.T / norms).T
assert max(numx.minimum(numx.sum(abs(poss - dir), axis=1), numx.sum(abs(poss + dir), axis=1))) < 1e-07, 'At least one node of the graph does lies out of the line.'
topolist = ng.graph.topological_sort()
deg = numx.asarray(map(lambda n: n.degree(), topolist))
idx = deg.argsort()
deg = deg[idx]
assert_equal(deg[:2], [1, 1])
assert_array_equal(deg[2:], [2 for i in xrange(len(deg) - 2)])
x0 = numx.outer(numx.amin(x, axis=0), dir) + const
x1 = numx.outer(numx.amax(x, axis=0), dir) + const
linelen = utils.norm2(x0 - x1)
dist = linelen / poss.shape[0]
nodes = ng.graph.undirected_dfs(topolist[idx[0]])
poss = numx.array(map(lambda n: n.data.pos, nodes))
dists = numx.sqrt(numx.sum((poss[:-1, :] - poss[1:, :]) ** 2, axis=1))
assert_almost_equal(dist, mean(dists), 1)
```

## 8. test_process_scheduler_flow

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/mdp/test/test_process_schedule.py:57`
- Note: Workflow: Test process scheduler with real Nodes.

```python
'Test process scheduler with real Nodes.'
precision = 6
node1 = mdp.nodes.PCANode(output_dim=20)
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
node3 = mdp.nodes.SFANode(output_dim=10)
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
input_dim = 30
scales = n.linspace(1, 100, num=input_dim)
scale_matrix = mdp.numx.diag(scales)
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
x = mdp.numx.random.random((10, input_dim))
with parallel.ProcessScheduler(verbose=False, n_processes=3, source_paths=None) as scheduler:
    parallel_flow.train(train_iterables, scheduler=scheduler)
    parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
flow.train(train_iterables)
assert parallel_flow[0].tlen == flow[0].tlen
y1 = flow.execute(x)
y2 = parallel_flow.execute(x)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## 9. test_thread_scheduler_flow

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/mdp/test/test_schedule.py:52`
- Note: Workflow: Test thread scheduler with real Nodes.

```python
'Test thread scheduler with real Nodes.'
precision = 6
node1 = mdp.nodes.PCANode(output_dim=20)
node2 = mdp.nodes.PolynomialExpansionNode(degree=1)
node3 = mdp.nodes.SFANode(output_dim=10)
flow = mdp.parallel.ParallelFlow([node1, node2, node3])
parallel_flow = mdp.parallel.ParallelFlow(flow.copy()[:])
scheduler = parallel.ThreadScheduler(verbose=False, n_threads=3)
input_dim = 30
scales = n.linspace(1, 100, num=input_dim)
scale_matrix = mdp.numx.diag(scales)
train_iterables = [n.dot(mdp.numx_rand.random((5, 100, input_dim)), scale_matrix) for _ in xrange(3)]
parallel_flow.train(train_iterables, scheduler=scheduler)
x = mdp.numx.random.random((10, input_dim))
parallel_flow.execute([x for _ in xrange(8)], scheduler=scheduler)
scheduler.shutdown()
flow.train(train_iterables)
assert parallel_flow[0].tlen == flow[0].tlen
y1 = flow.execute(x)
y2 = parallel_flow.execute(x)
assert_array_almost_equal(abs(y1), abs(y2), precision)
```

## 10. test_run_cmd_timeout

- Kind: `test-workflow`
- Source: `afni/tests/scripts/test_testing_script_functionality.py:171`
- Note: Workflow: test run cmd timeout

```python
data.logger = logging
monkeypatch.setattr(logging, 'warn', lambda x: None)
t_unit = 0.2
tools.run_cmd(data, f'sleep {t_unit * 10} & sleep {t_unit}; kill %1', timeout=t_unit * 2)
start = time.time()
with pytest.raises(TimeoutError):
    tools.run_cmd(data, f'sleep {t_unit} & sleep {t_unit}', timeout=t_unit * 0.5)
start = time.time()
with pytest.raises(TimeoutError):
    tools.run_cmd(data, f'sleep {t_unit * 500} & sleep {t_unit / 2}', timeout=t_unit)
delta_t = time.time() - start
assert delta_t < t_unit + 1.1
stdout_log, stderr_log = tools.run_cmd(data, f'sleep {t_unit / 2}; echo hello & sleep {t_unit / 5}', timeout=t_unit * 1)
assert stdout_log.read_text() == 'hello\n'
```

## 11. test_unparse_args_for_container

- Kind: `test-workflow`
- Source: `afni/tests/scripts/test_testing_script_functionality.py:1211`
- Note: Workflow: test unparse args for container

```python
user_args = {}
expected = ' local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'build_dir': '/saved/afni/build', 'debug': True, 'extra_args': None, 'ignore_dirty_data': False, 'image_name': 'afni/afni_cmake_build', 'source_mode': 'host', 'only_use_local': True, 'use_all_cores': False, 'coverage': True, 'verbose': False}
expected = ' --build-dir=/opt/afni/build --debug --coverage local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'debug': False, 'extra_args': '-k hello --trace', 'use_all_cores': False, 'coverage': True, 'verbose': False}
expected = ' --extra-args="-k hello --trace" --coverage local'
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert converted == expected
user_args = {'arbitrary_kwarg_with_underscores': True}
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert '--arbitrary-kwarg-with-underscores local' in converted
user_args = {'reuse_build': True}
converted = ce.unparse_args_for_container(TESTS_DIR, **user_args)
assert '--build-dir=/opt/afni/build' in converted
```

## 12. test_apply_affine

- Kind: `test-workflow`
- Source: `afni/src/pkundu/meica.libs/nibabel/tests/test_affines.py:27`
- Note: Workflow: test apply affine

```python
rng = np.random.RandomState(20110903)
aff = np.diag([2, 3, 4, 1])
pts = rng.uniform(size=(4, 3))
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]])
aff[:3, 3] = [10, 11, 12]
assert_array_equal(apply_affine(aff, pts), pts * [[2, 3, 4]] + [[10, 11, 12]])
aff[:3, :] = rng.normal(size=(3, 4))
exp_res = np.concatenate((pts.T, np.ones((1, 4))), axis=0)
exp_res = np.dot(aff, exp_res)[:3, :].T
assert_array_equal(apply_affine(aff, pts), exp_res)
assert_almost_equal(validated_apply_affine(aff, pts), apply_affine(aff, pts))
assert_array_equal(apply_affine(aff.tolist(), pts.tolist()), exp_res)
aff = np.array([[0, 2, 0, 10], [3, 0, 0, 11], [0, 0, 4, 12], [0, 0, 0, 1]])
pts = np.array([[1, 2, 3], [2, 3, 4], [4, 5, 6], [6, 7, 8]])
exp_res = (np.dot(aff[:3, :3], pts.T) + aff[:3, 3:4]).T
assert_array_equal(apply_affine(aff, pts), exp_res)
pts = pts.reshape((2, 2, 3))
exp_res = exp_res.reshape((2, 2, 3))
assert_array_equal(apply_affine(aff, pts), exp_res)
for N in range(2, 6):
    aff = np.eye(N)
    nd = N - 1
    aff[:nd, :nd] = rng.normal(size=(nd, nd))
    pts = rng.normal(size=(2, 3, nd))
    res = apply_affine(aff, pts)
    new_pts = np.ones((N, 6))
    new_pts[:-1, :] = np.rollaxis(pts, -1).reshape((nd, 6))
    exp_pts = np.dot(aff, new_pts)
    exp_pts = np.rollaxis(exp_pts[:-1, :], 0, 2)
    exp_res = exp_pts.reshape((2, 3, nd))
    assert_array_almost_equal(res, exp_res)
```
