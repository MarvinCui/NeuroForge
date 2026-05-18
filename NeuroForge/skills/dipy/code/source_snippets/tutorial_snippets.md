# dipy Tutorial Snippets

Curated implementation snippets recovered from the original generated output. Source paths are upstream-relative or package-relative, never local machine paths.

## 1. How To: Affreg All Transforms

- Kind: `tutorial`
- Source: `references/tutorials/affreg-all-transforms/affreg-all-transforms.md`
- Note: Workflow: test affreg all transforms

```python
# Setup
# Fixtures: rng

# Workflow
for ttype in sorted(factors):
    dim = ttype[1]
    if dim == 2:
        nslices = 1
    else:
        nslices = 45
    factor = factors[ttype][0]
    sampling_pc = factors[ttype][1]
    trans = regtransforms[ttype]
    srt = setup_random_transform
    static, moving, static_g2w, moving_g2w, smask, mmask, T = srt(trans, factor, nslices, 1.0, rng=rng)
    start_sad = np.abs(static - moving).sum()
    metric = imaffine.MutualInformationMetric(nbins=32, sampling_proportion=sampling_pc)
    affreg = imaffine.AffineRegistration(metric=metric, level_iters=[1000, 100, 50], sigmas=[3, 1, 0], factors=[4, 2, 1], method='L-BFGS-B', ss_sigma_factor=None, options=None)
    x0 = trans.get_identity_parameters()
    if sampling_pc not in [1.0, None]:
        affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
    else:
        affine_map = affreg.optimize(static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=smask, moving_mask=mmask)
    transformed = affine_map.transform(moving)
    end_sad = np.abs(static - transformed).sum()
    reduction = 1 - end_sad / start_sad
    print(f'{ttype}>>{reduction:f}')
    assert reduction > 0.9
metric = imaffine.MutualInformationMetric(nbins=32)
assert_raises(ValueError, imaffine.AffineRegistration, metric=metric, level_iters=[])
affine_map = assert_warns(UserWarning, affreg.optimize, static, moving, trans, x0, static_grid2world=static_g2w, moving_grid2world=moving_g2w, starting_affine=None, ret_metric=None, static_mask=np.zeros_like(smask), moving_mask=np.zeros_like(mmask))
```

## 2. How To: Em 2D Demons

- Kind: `tutorial`
- Source: `references/tutorials/em-2d-demons/em-2d-demons.md`
- Note: Workflow: Test 2D SyN with EM metric, demons-like optimizer Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good qua

```python
# Workflow
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

## 3. How To: Em 2D Gauss Newton

- Kind: `tutorial`
- Source: `references/tutorials/em-2d-gauss-newton/em-2d-gauss-newton.md`
- Note: Workflow: Test 2D SyN with EM metric, Gauss-Newton optimizer Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good qu

```python
# Workflow
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

## 4. How To: Bdg Get Direction

- Kind: `tutorial`
- Source: `references/tutorials/bdg-get-direction/bdg-get-direction.md`
- Note: Workflow: This tests the direction found by the bootstrap direction getter.

```python
# Workflow
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

## 5. How To: Validate Patch Radius And Version

- Kind: `tutorial`
- Source: `references/tutorials/validate-patch-radius-and-version/validate-patch-radius-and-version.md`
- Note: Workflow: test validate patch radius and version

```python
# Workflow
data = np.random.rand(5, 5, 5, 10)
bvals = np.zeros(10)
test_cases = [{'patch_radius': 1, 'version': 1, 'tmp_dir': None, 'expect_fail': False}, {'patch_radius': (1, 1, 1), 'version': 1, 'tmp_dir': None, 'expect_fail': False}, {'patch_radius': (0, 0, 0), 'version': 1, 'tmp_dir': None, 'expect_fail': False}, {'patch_radius': (0, 0, 0), 'version': 3, 'tmp_dir': None, 'expect_fail': False}, {'patch_radius': 1, 'version': 3, 'tmp_dir': None, 'expect_fail': True}, {'patch_radius': (1, 1, 1), 'version': 3, 'tmp_dir': None, 'expect_fail': True}, {'patch_radius': (0, 0, 0), 'version': 3, 'tmp_dir': '/nonexistent_dir', 'expect_fail': True}, {'patch_radius': 1, 'version': 1, 'tmp_dir': '/some_temp_dir', 'expect_fail': True}]
for case in test_cases:
    patch_radius = case['patch_radius']
    version = case['version']
    tmp_dir = case['tmp_dir']
    expect_fail = case['expect_fail']
    if expect_fail:
        with pytest.raises(ValueError):
            p2s.patch2self(data, bvals, patch_radius=patch_radius, version=version, tmp_dir=tmp_dir)
    else:
        try:
            result = p2s.patch2self(data, bvals, patch_radius=patch_radius, version=version, tmp_dir=tmp_dir)
            assert result.shape == data.shape, f'Shape mismatch with patch_radius={patch_radius}, version={version}, tmp_dir={tmp_dir}'
        except ValueError:
            pytest.fail(f'Unexpected ValueError with patch_radius={patch_radius}, version={version}, tmp_dir={tmp_dir}')
```

## 6. How To: Streamline Registration

- Kind: `tutorial`
- Source: `references/tutorials/streamline-registration/streamline-registration.md`
- Note: Workflow: test streamline registration

```python
# Setup
# Fixtures: rng

# Workflow
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

## 7. How To: Mapmri Isotropic Static Scale Factor

- Kind: `tutorial`
- Source: `references/tutorials/mapmri-isotropic-static-scale-factor/mapmri-isotropic-static-scale-factor.md`
- Note: Workflow: test mapmri isotropic static scale factor

```python
# Setup
# Fixtures: radial_order, rng

# Workflow
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

## 8. How To: Cc 3D

- Kind: `tutorial`
- Source: `references/tutorials/cc-3d/cc-3d.md`
- Note: Workflow: Test 3D SyN with CC metric Register a volume created by stacking copies of a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registratio

```python
# Workflow
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

## 9. How To: Mcsd Model Delta

- Kind: `tutorial`
- Source: `references/tutorials/mcsd-model-delta/mcsd-model-delta.md`
- Note: Workflow: test mcsd model delta

```python
# Workflow
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

## 10. How To: Diffeomorphic Map Simplification 2D

- Kind: `tutorial`
- Source: `references/tutorials/diffeomorphic-map-simplification-2d/diffeomorphic-map-simplification-2d.md`
- Note: Workflow: Test simplification of 2D diffeomorphic maps Create an invertible deformation field, and define a DiffeomorphicMap using different voxel-to-space transforms for domain, codomain, and reference discretizations, 

```python
# Workflow
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

## 11. How To: Cc 2D

- Kind: `tutorial`
- Source: `references/tutorials/cc-2d/cc-2d.md`
- Note: Workflow: Test 2D SyN with CC metric Register a coronal slice from a T1w brain MRI before and after warping it under a synthetic invertible map. We verify that the final registration is of good quality.

```python
# Workflow
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

## 12. How To: Mapmri Metrics Anisotropic

- Kind: `tutorial`
- Source: `references/tutorials/mapmri-metrics-anisotropic/mapmri-metrics-anisotropic.md`
- Note: Workflow: test mapmri metrics anisotropic

```python
# Setup
# Fixtures: radial_order

# Workflow
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
