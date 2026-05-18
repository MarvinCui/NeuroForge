# dipy Source/Test Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. test_bdg_get_direction

- Kind: `test-workflow`
- Source: `dipy/dipy/direction/tests/test_bootstrap_direction_getter.py:73`
- Note: Workflow: This tests the direction found by the bootstrap direction getter.

```python
'This tests the direction found by the bootstrap direction getter.'
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs, b0_threshold=0)
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
angles = [(0, 0)]
voxel, _ = multi_tensor(gtab, mevals, S0=1, angles=angles, fractions=[100], snr=100)
data = np.tile(voxel, (3, 3, 3, 1))
sphere = get_sphere(name='symmetric362')
response = (np.array([0.0015, 0.0003, 0.0003]), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    csd_model = ConstrainedSphericalDeconvModel(gtab, response, sh_order_max=6)
point = np.array([0.0, 0.0, 0.0])
prev_direction = sphere.vertices[5]
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10.0, sphere=sphere)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=10, sphere=sphere, max_attempts=3)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter(data, model=csd_model, max_angle=60.0, sphere=sphere, max_attempts=5)
    npt.assert_equal(boot_dg.get_direction(point, prev_direction), 0)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    npt.assert_raises(ValueError, lambda: BootDirectionGetter(data, csd_model, 60, sphere=sphere, max_attempts=0))
```

## 2. test_horizon

- Kind: `test-workflow`
- Source: `dipy/dipy/viz/tests/test_apps.py:95`
- Note: Workflow: test horizon

```python
s1 = 10 * np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0], [4, 0, 0]], dtype='f8')
s2 = 10 * np.array([[0, 0, 0], [0, 1, 0], [0, 2, 0], [0, 3, 0], [0, 4, 0]], dtype='f8')
s3 = 10 * np.array([[0, 0, 0], [1, 0.2, 0], [2, 0.2, 0], [3, 0.2, 0], [4, 0.2, 0]], dtype='f8')
streamlines = Streamlines()
streamlines.append(s1)
streamlines.append(s2)
streamlines.append(s3)
streamlines.shrink_data()
affine = np.array([[1.0, 0.0, 0.0, -98.0], [0.0, 1.0, 0.0, -134.0], [0.0, 0.0, 1.0, -72.0], [0.0, 0.0, 0.0, 1.0]])
data = 255 * rng.random((197, 233, 189))
vox_size = (1.0, 1.0, 1.0)
streamlines._data += np.array([-98.0, -134.0, -72.0])
header = create_nifti_header(affine, data.shape, vox_size)
sft = StatefulTractogram(streamlines, header, Space.RASMM)
tractograms = [sft]
images = None
with TemporaryDirectory() as out_dir:
    horizon(tractograms=tractograms, images=images, cluster=True, cluster_thr=5, random_colors=False, length_lt=np.inf, length_gt=0, clusters_lt=np.inf, clusters_gt=0, world_coords=True, interactive=False, out_png=Path(out_dir) / 'only-tractograms.png')
    images = [(data, affine, '/test/filename.nii.gz')]
    with npt.assert_raises(ValueError) as ve:
        horizon(tractograms=tractograms, images=images, cluster=True, cluster_thr=5, random_colors=False, length_lt=np.inf, length_gt=0, clusters_lt=np.inf, clusters_gt=0, world_coords=False, interactive=False, out_png=Path(out_dir) / 'native-tractograms.png')
    msg = 'Currently native coordinates are not supported for streamlines.'
    npt.assert_(msg in str(ve.exception))
    tractograms = None
    horizon(tractograms=tractograms, images=images, cluster=True, cluster_thr=5, random_colors=False, length_lt=np.inf, length_gt=0, clusters_lt=np.inf, clusters_gt=0, world_coords=True, interactive=False, out_png=Path(out_dir) / 'only-images.png')
    horizon(tractograms=tractograms, images=images, cluster=False, cluster_thr=5, random_colors=False, length_lt=np.inf, length_gt=0, clusters_lt=np.inf, clusters_gt=0, world_coords=True, interactive=False, out_png=Path(out_dir) / 'no-clusting-tractograms-and-images.png')
```

## 3. test_em_2d_demons

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_imwarp.py:1035`
- Note: Workflow: Test 2D SyN with EM metric, demons-like optimizer Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality.

```python
'Test 2D SyN with EM metric, demons-like optimizer\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 1
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
smooth = 2.0
inner_iter = 20
q_levels = 256
double_gradient = False
iter_type = 'demons'
metric = metrics.EMMetric(2, smooth=smooth, inner_iter=inner_iter, q_levels=q_levels, double_gradient=double_gradient, step_type=iter_type)
level_iters = [40, 20, 10]
optimizer = imwarp.SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None)
m = optimizer.get_map()
assert_equal(mapping, m)
s2ref, m2ref = optimizer.get_intermediate_maps()
assert_equal(s2ref, optimizer.static_to_ref)
assert_equal(m2ref, optimizer.moving_to_ref)
warped = mapping.transform(moving)
starting_energy = np.sum((static - moving) ** 2)
final_energy = np.sum((static - warped) ** 2)
reduced = 1.0 - final_energy / starting_energy
assert reduced > 0.9
```

## 4. test_em_2d_gauss_newton

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_imwarp.py:920`
- Note: Workflow: Test 2D SyN with EM metric, Gauss-Newton optimizer Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality.

```python
'Test 2D SyN with EM metric, Gauss-Newton optimizer\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 1
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
smooth = 5.0
inner_iter = 20
q_levels = 256
double_gradient = False
iter_type = 'gauss_newton'
metric = metrics.EMMetric(2, smooth=smooth, inner_iter=inner_iter, q_levels=q_levels, double_gradient=double_gradient, step_type=iter_type)
level_iters = [40, 20, 10]
optimizer = imwarp.SymmetricDiffeomorphicRegistration(metric, level_iters=level_iters)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None)
m = optimizer.get_map()
assert_equal(mapping, m)
s2ref, m2ref = optimizer.get_intermediate_maps()
assert_equal(s2ref, optimizer.static_to_ref)
assert_equal(m2ref, optimizer.moving_to_ref)
warped = mapping.transform(moving)
starting_energy = np.sum((static - moving) ** 2)
final_energy = np.sum((static - warped) ** 2)
reduced = 1.0 - final_energy / starting_energy
assert reduced > 0.9
```

## 5. test_streamline_registration

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_api.py:317`
- Note: Workflow: test streamline registration

```python
sl1 = [np.array([[0, 0, 0], [0, 0, 0.5], [0, 0, 1], [0, 0, 1.5]]), np.array([[0, 0, 0], [0, 0.5, 0.5], [0, 1, 1]])]
affine_mat = np.eye(4)
affine_mat[:3, 3] = rng.standard_normal(3)
sl2 = list(transform_tracking_output(sl1, affine_mat))
aligned, matrix = streamline_registration(sl2, sl1)
npt.assert_almost_equal(matrix, np.linalg.inv(affine_mat))
npt.assert_almost_equal(aligned[0], sl1[0])
npt.assert_almost_equal(aligned[1], sl1[1])
base_aff = np.eye(4) * rng.random()
base_aff[:3, 3] = np.array([1, 2, 3])
base_aff[3, 3] = 1
with TemporaryDirectory() as tmpdir:
    for use_aff in [None, base_aff]:
        fname1 = Path(tmpdir) / 'sl1.trx'
        fname2 = Path(tmpdir) / 'sl2.trx'
        if use_aff is not None:
            img = nib.Nifti1Image(np.zeros((2, 2, 2)), use_aff)
            tgm1 = StatefulTractogram(transform_tracking_output(sl1, np.linalg.inv(use_aff)), img, Space.VOX)
            save_tractogram(tgm1, fname1, bbox_valid_check=False)
            tgm2 = StatefulTractogram(transform_tracking_output(sl2, np.linalg.inv(use_aff)), img, Space.VOX)
            save_tractogram(tgm2, fname2, bbox_valid_check=False)
        else:
            img = nib.Nifti1Image(np.zeros((2, 2, 2)), np.eye(4))
            tgm1 = StatefulTractogram(sl1, img, Space.RASMM)
            tgm2 = StatefulTractogram(sl2, img, Space.RASMM)
            save_tractogram(tgm1, fname1, bbox_valid_check=False)
            save_tractogram(tgm2, fname2, bbox_valid_check=False)
        aligned, matrix = streamline_registration(fname2, fname1)
        npt.assert_almost_equal(aligned[0], sl1[0], decimal=5)
        npt.assert_almost_equal(aligned[1], sl1[1], decimal=5)
```

## 6. test_cc_3d

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_imwarp.py:801`
- Note: Workflow: Test 3D SyN with CC metric Register a volume created by stacking copies of a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality.

```python
'Test 3D SyN with CC metric\n\n    Register a volume created by stacking copies of a coronal slice from\n    a T1w brain MRI before and after warping it under a synthetic\n    invertible map. We verify that the final registration is of good\n    quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 21
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
sigma_diff = 2.0
radius = 2
similarity_metric = metrics.CCMetric(3, sigma_diff=sigma_diff, radius=radius)
level_iters = [20, 5]
step_length = 0.25
opt_tol = 0.0001
inv_iter = 20
inv_tol = 0.001
ss_sigma_factor = 0.2
optimizer = imwarp.SymmetricDiffeomorphicRegistration(similarity_metric, level_iters=level_iters, step_length=step_length, ss_sigma_factor=ss_sigma_factor, opt_tol=opt_tol, inv_iter=inv_iter, inv_tol=inv_tol)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None, moving_grid2world=None, prealign=None)
m = optimizer.get_map()
assert_equal(mapping, m)
s2ref, m2ref = optimizer.get_intermediate_maps()
assert_equal(s2ref, optimizer.static_to_ref)
assert_equal(m2ref, optimizer.moving_to_ref)
warped = mapping.transform(moving)
starting_energy = np.sum((static - moving) ** 2)
final_energy = np.sum((static - warped) ** 2)
reduced = 1.0 - final_energy / starting_energy
assert reduced > 0.9
```

## 7. test_mcsd_model_delta

- Kind: `test-workflow`
- Source: `dipy/dipy/reconst/tests/test_mcsd.py:74`
- Note: Workflow: test mcsd model delta

```python
sh_order_max = 8
gtab = get_3shell_gtab()
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    response = multi_shell_fiber_response(sh_order_max, [0, 1000, 2000, 3500], wm_response, gm_response, csf_response)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model = MultiShellDeconvModel(gtab, response)
iso = response.iso
theta, phi = (default_sphere.theta, default_sphere.phi)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    B = shm.real_sh_descoteaux_from_index(response.m_values, response.l_values, theta[:, None], phi[:, None])
wm_delta = model.delta.copy()
wm_delta[:iso] = 0.0
wm_delta = _expand(model.m_values, iso, wm_delta)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    for i, s in enumerate([0, 1000, 2000, 3500]):
        g = GradientTable(default_sphere.vertices * s)
        signal = model.predict(wm_delta, gtab=g)
        expected = np.dot(response.response[i, iso:], B.T)
        npt.assert_array_almost_equal(signal, expected)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    signal = model.predict(wm_delta, gtab=gtab)
fit = model.fit(signal)
m = model.m_values
npt.assert_array_almost_equal(fit.shm_coeff[m != 0], 0.0, 2)
```

## 8. test_mapmri_isotropic_static_scale_factor

- Kind: `test-workflow`
- Source: `dipy/dipy/reconst/tests/test_mapmri.py:374`
- Note: Workflow: test mapmri isotropic static scale factor

```python
gtab = get_gtab_taiwan_dsi()
D = 0.0007
tau = 1 / (4 * np.pi ** 2)
mu = np.sqrt(D * 2 * tau)
l1, l2, l3 = [D, D, D]
S = single_tensor(gtab, evals=np.r_[l1, l2, l3], rng=rng)
S_array = np.tile(S, (5, 1))
stat_weight = 0.1
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    mapm_scale_stat_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=False, static_diffusivity=D, laplacian_regularization=True, laplacian_weighting=stat_weight)
    mapm_scale_adapt_reg_stat = MapmriModel(gtab, radial_order=radial_order, anisotropic_scaling=False, dti_scale_estimation=True, laplacian_regularization=True, laplacian_weighting=stat_weight)
start = time.time()
mapf_scale_stat_reg_stat = mapm_scale_stat_reg_stat.fit(S_array)
time_scale_stat_reg_stat = time.time() - start
start = time.time()
mapf_scale_adapt_reg_stat = mapm_scale_adapt_reg_stat.fit(S_array)
time_scale_adapt_reg_stat = time.time() - start
assert_equal(np.all(mapf_scale_stat_reg_stat.mu == mu), True)
if not platform.system() == 'Windows':
    assert_equal(time_scale_stat_reg_stat < time_scale_adapt_reg_stat, True, f'mapf_scale_stat_reg_stat ({time_scale_stat_reg_stat}s) slower than mapf_scale_adapt_reg_stat ({time_scale_adapt_reg_stat}s). It should be the opposite.')
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    assert_almost_equal(mapf_scale_stat_reg_stat.fitted_signal(), mapf_scale_adapt_reg_stat.fitted_signal())
```

## 9. test_diffeomorphic_map_simplification_2d

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_imwarp.py:209`
- Note: Workflow: Test simplification of 2D diffeomorphic maps Create an invertible deformation field, and define a DiffeomorphicMap using different voxel-to-space transforms for domain, codomain, and reference discretizations, also use a non-identity pre-aligning matrix. Warp a circle using the diffeomorphic map to obtain the expected warped circle. Now simplify the DiffeomorphicMap and warp the same circle using this simplified map. Verify that the two warped circles are equal up to numerical precision.

```python
'Test simplification of 2D diffeomorphic maps\n\n    Create an invertible deformation field, and define a DiffeomorphicMap\n    using different voxel-to-space transforms for domain, codomain, and\n    reference discretizations, also use a non-identity pre-aligning matrix.\n    Warp a circle using the diffeomorphic map to obtain the expected warped\n    circle. Now simplify the DiffeomorphicMap and warp the same circle\n    using this simplified map. Verify that the two warped circles are equal\n    up to numerical precision.\n    '
dom_shape = (64, 64)
cod_shape = (80, 80)
nr = dom_shape[0]
nc = dom_shape[1]
s = 1.1
t = 0.25
trans = np.array([[1, 0, -t * nr], [0, 1, -t * nc], [0, 0, 1]])
trans_inv = np.linalg.inv(trans)
scale = np.array([[1 * s, 0, 0], [0, 1 * s, 0], [0, 0, 1]])
gt_affine = trans_inv.dot(scale.dot(trans))
radius = 16
circle = vfu.create_circle(cod_shape[0], cod_shape[1], radius)
d, dinv = vfu.create_harmonic_fields_2d(dom_shape[0], dom_shape[1], 0.3, 6)
D = gt_affine
C = imwarp.mult_aff(gt_affine, gt_affine)
R = np.eye(3)
P = gt_affine
diff_map = imwarp.DiffeomorphicMap(dim=2, disp_shape=dom_shape, disp_grid2world=R, domain_shape=dom_shape, domain_grid2world=D, codomain_shape=cod_shape, codomain_grid2world=C, prealign=P)
diff_map.forward = np.array(d, dtype=floating)
diff_map.backward = np.array(dinv, dtype=floating)
expected = diff_map.transform(circle, interpolation='linear')
simplified = diff_map.get_simplified_transform()
warped = simplified.transform(circle, interpolation='linear')
assert_array_almost_equal(warped, expected)
assert_equal(simplified.domain_grid2world, None)
assert_equal(simplified.codomain_grid2world, None)
assert_equal(simplified.disp_grid2world, None)
assert_equal(simplified.domain_world2grid, None)
assert_equal(simplified.codomain_world2grid, None)
assert_equal(simplified.disp_world2grid, None)
```

## 10. test_cc_2d

- Kind: `test-workflow`
- Source: `dipy/dipy/align/tests/test_imwarp.py:760`
- Note: Workflow: Test 2D SyN with CC metric Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality.

```python
'Test 2D SyN with CC metric\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 1
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
sigma_diff = 3.0
radius = 4
metric = metrics.CCMetric(2, sigma_diff=sigma_diff, radius=radius)
level_iters = [15, 5]
optimizer = imwarp.SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None)
m = optimizer.get_map()
assert_equal(mapping, m)
s2ref, m2ref = optimizer.get_intermediate_maps()
assert_equal(s2ref, optimizer.static_to_ref)
assert_equal(m2ref, optimizer.moving_to_ref)
warped = mapping.transform(moving)
starting_energy = np.sum((static - moving) ** 2)
final_energy = np.sum((static - warped) ** 2)
reduced = 1.0 - final_energy / starting_energy
assert reduced > 0.9
```

## 11. test_mapmri_metrics_anisotropic

- Kind: `test-workflow`
- Source: `dipy/dipy/reconst/tests/test_mapmri.py:551`
- Note: Workflow: test mapmri metrics anisotropic

```python
gtab = get_gtab_taiwan_dsi()
l1, l2, l3 = [0.0015, 0.0003, 0.0003]
S, _ = generate_signal_crossing(gtab, l1, l2, l3, angle2=0)
mapm = MapmriModel(gtab, radial_order=radial_order, laplacian_regularization=False)
mapfit = mapm.fit(S)
tau = 1 / (4 * np.pi ** 2)
rtpp_gt = 1.0 / (2 * np.sqrt(np.pi * l1 * tau))
rtap_gt = 1.0 / (2 * np.sqrt(np.pi * l2 * tau)) * 1.0 / (2 * np.sqrt(np.pi * l3 * tau))
rtop_gt = rtpp_gt * rtap_gt
msd_gt = 2 * (l1 + l2 + l3) * tau
qiv_gt = 64 * np.pi ** (7 / 2.0) * (l1 * l2 * l3 * tau ** 3) ** (3 / 2.0) / ((l2 * l3 + l1 * (l2 + l3)) * tau ** 2)
assert_almost_equal(mapfit.rtap(), rtap_gt, 5)
assert_almost_equal(mapfit.rtpp(), rtpp_gt, 5)
assert_almost_equal(mapfit.rtop(), rtop_gt, 5)
with warnings.catch_warnings(record=True) as w:
    ng = mapfit.ng()
    ng_parallel = mapfit.ng_parallel()
    ng_perpendicular = mapfit.ng_perpendicular()
    assert_equal(len(w), 3)
    for l_w in w:
        assert_(issubclass(l_w.category, UserWarning))
        assert_('model bval_threshold must be lower than 2000'.lower() in str(l_w.message).lower())
assert_almost_equal(ng, 0.0, 5)
assert_almost_equal(ng_parallel, 0.0, 5)
assert_almost_equal(ng_perpendicular, 0.0, 5)
assert_almost_equal(mapfit.msd(), msd_gt, 5)
assert_almost_equal(mapfit.qiv(), qiv_gt, 5)
```

## 12. test_orthogonality_basis_functions

- Kind: `test-workflow`
- Source: `dipy/dipy/reconst/tests/test_mapmri.py:55`
- Note: Workflow: test orthogonality basis functions

```python
diffusivity = 0.0015
qmin = 0
qmax = 1000
int1 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(0, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)), qmin, qmax)[0]
int2 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)), qmin, qmax)[0]
int3 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)), qmin, qmax)[0]
int4 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(8, x, diffusivity)), qmin, qmax)[0]
assert_almost_equal(int1, 0.0)
assert_almost_equal(int2, 0.0)
assert_almost_equal(int3, 0.0)
assert_almost_equal(int4, 0.0)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', category=integrate.IntegrationWarning)
    int1 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(1, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int2 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int3 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int4 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(5, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
assert_almost_equal(int1, 0.0)
assert_almost_equal(int2, 0.0)
assert_almost_equal(int3, 0.0)
assert_almost_equal(int4, 0.0)
```
